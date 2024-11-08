### 1. 查看文件信息
* ll - a  查看隐藏文件
* ls -lah 查看所有文件
* mkdir -p /build/a/b  递归创建文件   
### 2. tree  
    sudo apt-get install tree
    tree
 
### 3. 查找命令
    1) 在当前目录查找某个文件：find . -name "文件名"
    2) 在当前目录查找某个文件：find . -name "a*" // 查找以a为前缀
    3) 在所有路径下查找某文件：find / -name "文件名"

### 4. 换行符(vs code右下角状态栏) 
    windows CRLF \r\n
    Linux LF \n

### 5. linux文件解压缩  
    压缩文件：tar -czvf archive.tar.gz /path/to/file_or_folder
    解压文件：tar -xzvf archive.tar.gz
        -c：创建新的压缩文件
        -z：使用gzip压缩
        -j：使用bzip2压缩
        -v：显示详细信息
        -f：指定文件名

### 6. linux设备之间传输文件
    1) scp /path/to/file username@destination:/path/to/destination
    2) rsync -avz /path/to/file username@destination:/path/to/destination

### 7. 将压缩包解压到指定位置
tar -zxvf archive.tar.gz -C /path/to/destination
unzip -d /temp test.zip

### 8. 释放win的空间
1） 检查出内存大于2G的文件夹
Get-ChildItem -Path D:\ -Recurse -File -ErrorAction SilentlyContinue | 
Where-Object { $_.Length -gt 1GB } | 
Select-Object FullName, @{Name="Size(GB)";Expression={[math]::Round($_.Length / 1GB, 2)}} |
Format-Table -AutoSize

vmware-vdiskmanager -R "D:\vmware\ubuntu22_atc\Ubuntu22_atc.vmdk"
