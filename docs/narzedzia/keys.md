# Klucze prywatne / publiczne

**Wygenerowanie nowej pary kluczy prywatny / publiczny**

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/ssh-key-file-name
```

**Wygenerowanie 2048 bitowego klucza RSA**

```
openssl genrsa -des3 -out private.pem 2048
```

**Wygenrowanie publicznego klucza z klucza prywatnego**

```
openssl rsa -in private.pem -outform PEM -pubout -out public.pem
```