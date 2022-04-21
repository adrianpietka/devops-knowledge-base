# Linux Cheet Sheet

**New line into echo**

```
echo -e "Create the snapshots\n\nSnapshot created"
```

**Redirect error and output messages to /dev/null**

```
command > /dev/null 2>&1
```

**Generate random number from a range**

```
shuf -i 2000-65000 -n 1
```

**Tworzenie folderów**

***Utworzenie folderu z ustawionym chmod***

mkdir -m 777 /path/to/your/dir

***Utworzenie pełnego drzewa folderów***

mkdir -p /parent/dirs/to/create/your/dir