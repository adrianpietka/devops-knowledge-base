# Kubernetes

- Platforma która pozwala pisać aplikacje w modelu Cloud-Native niezależnie od tego jak ten Twój Cloud wygląda
- Kiedy wybierać? Zdać sobie pytania:
  - Gdzie chcemy być?
  - Jak chcemy aby nasza aplikacja się rozrastała?

## Podstawowe polecenia

- `kubectl get pod -w`
- `kubectl apply -f xxx.yaml`
- `kubectl get ing`
- `kubectl get ns`
- `kubectl get pv`
- `kubectl delete ns [name]`
- `kubectl create namespace [name]`
- `kubectl apply -f xxx.yaml -n [namespace name]`

## Pod

- Idempotentny - nie da się go zmienić, jeśli chcemy zmienić trzeba go usunąć i dodać na nowo
- Efemeryczny - dane mogą zniknąć
- Najmniejsza jednostka w Kubernetes - składająca się zazwyczaj z jednego kontenera, w uzasadnionych przypadkach z więcej, można spotkać rozwiązania oparte o:
  - SideCar Container - np. firewall dla kontenera drop packet lub puść ruch do drugiego kontenera
  - Init Container - np. inicjalizacja cache, bazy danych i umiera
- Kontenery w pod współużytkują stos sieciowy, nie mają osobnych adresów IP, mogą komunikować się po hostname = localhost

## ReplicaSet

- Tworzenie podów względem ilości wymaganych replik
- Wykorzystuje etykiety
- Oparty o szablon dla poda
- Kontroluje aby odpowiednia ilość podów działała
- Nazwa ReplicaSet używana jako prefix dla kontrolowanych podów
- Autoskalowanie w zależności od zapotrzebowania
  - Przy użyciu np. metryki średniego użycia CPU 

## Service

- Grupuje pody o określonych etykietach
- Z usługą skojarzona jest nazwa DNSowa ([usługa].[projekt].svc.cluster.local)
- Typy
  - `ClusterIp` - specjalny adres IP widoczny tylko wewnątrz klastra, dla usług działających na klastrze, zgrupowanie podów pod adresem IP
  - `NodePort` - dostanie się do podów za pomocą jednego z portów wystawionych na node (nawet jeśli pod na danym node nie jest udostępniony to port jest zarezerwowany), porty dostępne są również na zewnątrz klastra
  - `LoadBalancer` - automatyczna komunikacja poprzez API z infrastrukturą w której działa Kubernetes (np. jeśli na AWS to woła Classic Load Balancer)
  - `ExternalName` - referencja do jakiejś nazwy DNSowej

## Ingress

- Reverse Proxy
- Służy do terminowania ruchu po HTTP/HTTPS kierując go do Service
- Możliwość wyboru implementacji Ingress np. ngixn, HaProxy, Traefik
- Łatwość konfiguracji - za pomocą annotacji

## Deployment - Rolling Update

- Tworzy nowy ReplicaSet z podami i czeka aż pody zostaną utworzone, ze starego ReplcaSet usuwane są pody
- readinessProbe - upewnianie się czy aplikacja działa, bo np. aplikacja może długo wstawać (request na konkretny url)

## ConfigMap

- Dostarczanie konfiguracji za pomocą zmiennych środowiskowych do kontenera
- Można zamontować ConfigMap do filesystemu jako zwykły plik (np. konfiguracja dla aplikacji /etc/nginx itp.) 
- `kubectl create configmap xxx-name-yyy --from-file=nazwapliku.json`

## Secret

- Przeznaczony do przechowywania wrażliwych danych - hasła, OAuth token, klucz SSH

## Namespace

- Wirtualne środowiska - development, test, production
- Separacja obiektów, żeby się obiekty między sobą nie widziały, prawa użytkowników do namespace, reguły ograniczające (quoty) CPU, RAM dla poda
- Domyślny namespace = default

## Volumes

- Można podmontować katalog na serwerze lokalnym (volumePath) oraz zdalnym (nfs)
- Persistent Volumes
  - Persistent Volume Claim - warstwa abstrakcji, żądanie przydzielenia wolumenu, szuka dostępnych wolumentów tak aby spełnić żądanie przydzielenia
  - Storage Class - charakteryzacja Persistent Volumes (np. opisujemy slow, cloud, etc)
  - Persistent Volume tworzony za pomocą pluginów m.in: NFS, CephFS, Cinder, AWS Elastic Block Store, Azure Disk, Vsphere Volume, GCE Persistent Disk, iSCSI
  - Wtedy pod nie definiuje gdzie zapisuje dane
  - Wolumeny dynamic (stawiany dynamicznie) oraz static pool (definiowane)

## Minikube

- Uruchamianie małego klastra na swoim komputerze
- Potrzebuje hypervisora np. HyperV, VirtualBox
- Uruchamia maszynę wirtualna, a wewnątrz niej Kubernetes
- https://github.com/kubernetes/minikube

## Web UI

- https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
- Zestawienie:
  - `kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/aio/deploy/recommended/kubernetes-dashboard.yaml`
  - `kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | awk '/^deployment-controller-token-/{print $1}') | awk '$1=="token:"{print $2}'`
  - `kubectl proxy`
- Heapster - Zbieranie metryk

## Stern

- Podgląd logów dla całego poda
- Koloryzacja, tailowanie oraz wyświetlanie logów
- https://github.com/wercker/stern

## Helm

- Paczkowanie i wersjonowanie yamli opisujących środowisko (paczka jako tar.gz) oraz dostarczanie parametrów
- Helm (cli client) + Tiller (server) (wersji 3 będzie bez Tillera, wystarczy cli)
- Charts - paczka
- Helm repository - repozytorium stabilne i inkubator
  - https://github.com/helm/charts
  - https://hub.kubeapps.com/
- Tworzy releasy w momencie uruchamiania paczki

## Helm Chart dla własnych aplikacji

- Chartmuseum - własne repozytorium
- `helm-push` plugin do pushowania paczek do repozytorium
- `helm create mychart`
- `helm repo list`
- `helm search [name]`
- `helm repo update`
- `helm ls`

## Linki

- https://cloudowski.com/kubernetes-po-polsku
- https://devstyle.pl/2019/04/15/devtalk-94-o-kubernetes-z-karolem-stepniewskim/
- https://www.youtube.com/watch?v=ysk_2w_diKY
- https://blog.gutek.pl/2018/02/26/kubernetes-slownik-pojec/
