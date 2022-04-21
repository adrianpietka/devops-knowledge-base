# SSH

**Uruchomienie agenta start the ssh-agent in the background**

```
eval "$(ssh-agent -s)"
```

**Dodanie klucza tak aby był widzany podczas nawiązywania połączeń**

```
ssh-add ~/.ssh/ssh-key-file-name
```