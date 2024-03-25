# Solution to Lab3b

## Scpriting

```bash
# phonebook.sh
#!/bin/bash

flag=$1
case "$flag" in
    new)
    		# check arg count
        if [ $# -ne 3 ]; then
            echo "Usage: $0 new name tel"
        else
            echo "$2 $3" >> phonebook.txt
        fi
        ;;
    list)
        if [ ! -s phonebook.txt ]; then
            echo "phonebook is empty"
        else
            cat phonebook.txt
        fi
        ;;
    lookup)
        if [ $# -ne 2 ]; then
            echo "Usage: $0 lookup name"
        else
            name=$2
            # use grep to get matched name and its
            # corresponding tel number
            result=$(grep -i "^$name " phonebook.txt)
            # use -z to check whether result is empty
            if [ -z "$result" ]; then
                echo "No entry found for $name"
            else
                echo "$result"
            fi
        fi
        ;;
    remove)
        if [ $# -ne 2 ]; then
            echo "Usage: $0 remove name"
        else
            name=$2
            if ! grep -iq "^$name " phonebook.txt; then
                echo "No entry found for $name to remove"
            else
                # use sed to delete matched name
                sed -i "/^$name /Id" phonebook.txt
                echo "Entry for $name removed"
            fi
        fi
        ;;
    *)
    		# handle unexpected cases
        echo "Unknown command: $1"
        echo "Usage: $0 [new] [list] [lookup] [remove]"
        ;;
esac
```
