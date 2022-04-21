# SSH

**Uruchomienie agenta start the ssh-agent in the background**

```
eval "$(ssh-agent -s)"
```

**Dodanie klucza tak aby był widzany podczas nawiązywania połączeń**

```
ssh-add ~/.ssh/ssh-key-file-name
```

**Uprawnienia folderu i plików z kluczami**

- `.ssh` directory: 700 (`drwx------`)
- public key (`.pub` files): 644 (`-rw-r--r--`)
- private key (`id_rsa`): 600 (`-rw-------`)
- list of authorized keys (`authorized_keys` file): 600 (`-rw-------`)
- config (`config` file): 600 (`-rw-------`)
- lastly your home directory should not be writeable by the group or others (at most 755 (`drwxr-xr-x`))

Polecenia do zmiany uprawnień:

```
sudo chmod 700 ~/.ssh
sudo chmod 644 ~/.ssh/id_example.pub
sudo chmod 600 ~/.ssh/id_example
```