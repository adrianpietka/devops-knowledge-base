# Linux Cheet Sheet

## Róźne

**New line into echo**

```
echo -e "Create the snapshots\n\nSnapshot created"
```

**Run the last command as sudo**

```
sudo !!
```

**Generate random number from a range**

```
shuf -i 2000-65000 -n 1
```

## Stream redirects

```> file``` - redirects stdout to file

```1> file``` - redirects stdout to file

```2> file``` - redirects stderr to file

```&> file``` - redirects stdout and stderr to file

**Redirect error and output messages to /dev/null**

```
command > /dev/null 2>&1
```

## Chmod

https://chmod-calculator.com/

```
d rwx rwx rwx
- --- --- ---
|  |   |   |__ wszyscy użytkownicy
|  |   |__ uprawnienia grupy
|  |__ uprawnienia właściciela
|__ typ
```

## Grupy i użytkownicy

**List groups of user**

```
groups [username]
id [username]
```

**Add a new group**

```
groupadd [groupname]
```

**Add user to sudoers**

```
sudo adduser <username> sudo
```

**Add an existing user to a group**

```
usermod -a -G [groupname] [username]
```

**Change ownership and group of directory**

```
chown -R username:group directory
```

## Environment variables

```bash
export ENV_NAME=value
echo $ENV_NAME
printenv
```

## Filesystem

**Find number of files in folder and sub folders**

```
find . -type f | wc -l

29360

tree . | tail -1

3556 directories, 28009 files
```

**Faster creating backup of file**

```
cp config.cfg{,.bak}
```

**Create or update a symlink**

```
ln -sf /path/to/file /path/to/symlink
```

## Tworzenie folderów

***Utworzenie folderu z ustawionym chmod***

```
mkdir -m 777 /path/to/your/dir
```

***Utworzenie pełnego drzewa folderów***

```
mkdir -p /parent/dirs/to/create/your/dir
```

## apt-get

**Check the version before install packages using apt-get**

```
apt-cache policy <package-name>
```
