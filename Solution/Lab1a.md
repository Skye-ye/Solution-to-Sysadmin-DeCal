# Solution to Lab1a
## Question 1
```bash
curl -s https://raw.githubusercontent.com/0xcf/decal-labs/master/a1/albums.txt | \
    grep ', Future' | \
    cut -d',' -f1 | \
    while read album; \
    do mkdir -p "$album"; \
    done
```
## Question 2
```bash
# car.sh
#!/bin/bash
   
first_dir="${1#/}"
first_dir="${first_dir%%/*}"
   
echo "$first_dir"
```

```bash
# cdr.sh
#!/bin/bash
   
echo "${1##*/}"
```
## Question 3
```bash
# rename.sh
#!/bin/bash
   
if [ "$#" -ne 3 ]; then
    echo "Usage: $0 <directory> <original extension> <new extension>"
    exit 1
fi
   
directory=$1
original=$2
new=$3
   
if [ "$original" = "$new" ]; then
    echo "Original and new extensions are the same. No files to rename."
    exit 0
fi
   
cd "$directory" || { echo "Directory not found"; exit 1; }
   
for file in *.$original; do
    newfile="${file%.$original}.$new"
    if [ -f "$file" ]; then
        echo "renaming $directory/$file to $directory/$newfile"
        mv "$file" "$newfile"
    fi
done
```
## Question 4
```bash
# mkrandom.sh
#!/bin/bash
   
if [ "$#" -ne 2 ]; then
    echo "Usage: $0 <number of files> <size of each file in bytes>"
    exit 1
fi
   
num=$1
size=$2
   
for ((i = 1; i <= $num; i++)); do
    head -c "$size" /dev/urandom > "$i"
done
```
