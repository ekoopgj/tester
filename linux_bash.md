# 1.创建新目录

```shell
mkdir -p tester{1..10}
ls
```

# 2.切换到新目录下

``` shell
cd tester1
cd ../
```

# 3.创建新文件，在新文件中添加内容

```shell
touch template{1..10}.txt
ls
vim template1.txt
cat template1.txt 
```

# 4.查看新文件中的内容

```shell
less template1.txt 
ls -al template1.txt 
chmod 777 template1.txt 
ls -al template1.txt 
```

# 5. 修改新文件权限为可读、可写、可执行

```shell
chmod +rwx template2.txt 
ls -al template2.txt 
```

# 6.查看当前目录

```shell
pwd
```

# 查询 Linux 系统负载与进程

```shell
ps aux
```

# 查询 Linux 系统内存使用数据并保存到文件中

```shell
free -h > memory_usage.txt
```

# 统计内存数据文件的字节数

```shell
wc -c memory_usage.txt
```

# 对内存数据文件的每一行按 ASCII 码值降序排列并去重

```shell
tr -cd '\11\12\15\40-\176' < memory_usage.txt | sort -r | uniq
```

# 查询 Linux 系统进程列表快照

```shell
ps aux --sort=-%cpu`
htop
```

# 统计 /home 目录下不同用户的普通文件的总数是多少

```shell
find /home -maxdepth 1 -mindepth 1 -type d | while read userdir; do     user=$(basename "$userdir");     count=$(find "$userdir" -maxdepth 1 -type f | wc -l);     echo "$user $count"; done
```

# 统计 netstat -anp 状态为 LISTEN 和 CONNECT 的连接数量分别是多少

```shell
echo "LISTEN: $(netstat -anp | grep LISTEN | wc -l), ESTABLISHED: $(netstat -anp | grep ESTABLISHED | wc -l)"
LISTEN: 43, ESTABLISHED: 2
```

# 使用 bash 实现自动创建目录并生成文件 & 判断目录是否存在

```shell
#!/bin/bash
# ========================================================
# Author: Eric
# Date: [2025-03-29]
# Description: This script automatically creates a directory
#              and generates a file inside it.
# Applicable System: Linux / macOS
# Usage:
#   1. Grant execution permission: chmod +x create_dir_and_file.sh
#   2. Run the script: ./create_dir_and_file.sh
# ========================================================

# Set the target directory and file name
TARGET_DIR="/home/ck305271/test_dir"
FILE_NAME="example.txt"

# Check if the directory exists, create it if not
if [ ! -d "$TARGET_DIR" ]; then
    mkdir -p "$TARGET_DIR"
    echo "Directory created: $TARGET_DIR"
else
    echo "Directory already exists: $TARGET_DIR"
fi

# Create the file in the directory
FILE_PATH="$TARGET_DIR/$FILE_NAME"
if [ ! -f "$FILE_PATH" ]; then
    touch "$FILE_PATH"
    echo "File created: $FILE_PATH"
else
    echo "File already exists: $FILE_PATH"
fi

echo "Hello, this is a test file." > "$FILE_PATH"
echo "文File content written: $FILE_PATH"

```

