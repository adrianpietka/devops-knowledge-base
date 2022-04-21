# Bash Cheat Sheet

**Instrukcje warunkowe**

Using the [[ ... ]] test construct, rather than [ ... ] can prevent many logic errors in scripts. For example, the &&, ||, <, and > operators work within a [[ ]] test, despite giving an error within a [ ] construct.

```
if [[ -d "${DIRECTORY}" && ! -L "${DIRECTORY}" ]] ; then
    echo "It's a bona-fide directory"
fi
```

*To check if a directory exists*

```
if [ -d "$DIRECTORY" ]; then
  # Control will enter here if $DIRECTORY exists.
fi
```

*Check if a directory doesn't exist*

```
if [ ! -d "$DIRECTORY" ]; then
  # Control will enter here if $DIRECTORY doesn't exist.
fi
```

*Check if file does not exist*

```
if [[ ! -f /tmp/foo.txt ]]; then
    echo "File not found!"
fi
```