скрипт, который на вход принимает путь к директории, и выводит рекурсивно, содержащиеся в
ней файлы и директории со статистикой:
для файлов: размер в байтах, контрольная сумма
для директорий: количество файлов, общий размер директории

```
#!/bin/bash
target_path=$1

if [ -z $1 ]; then
echo "Usage: $0 </path/to/dir>"
exit 1
fi
function get_files_count {
count=$(ls -l $1 | awk ’NR!=1 {print}’ | wc -l)
echo -e "$1: files count - ${count}\tsize - $(du -hs $1 | awk ’{print $1}’)" | tr -s /
}
function check_type {
type=$(stat --printf=%F $1)
if [ "$type" == "directory" ]; then
return 1
else
return 2
fi
}
function get_file_stat {
size=$(stat --printf="%s" $1)
checksum=$(shasum -a256 $1 | awk ’{print $1}’)
echo -e "$1: size - ${size}\tchecksum - ${checksum}" | tr -s /
}
function dir_roll {
get_files_count $1
files=$(ls -l $1 | awk ’NR!=1{print $9}’)
for f in $files
do
is_dir_or_file=$(check_type $1/$f; echo $?)
if [ "$is_dir_or_file" == "1" ]; then
dir_roll $1/$f
else
get_file_stat $1/$f
fi
done
}
dir_roll $target_path
```
