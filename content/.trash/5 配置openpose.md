## libatlas-base-dev 无法安装
添加 `contrib` 和 `non-free` 源

```bash
sudo nano /etc/apt/sources.list
```

将下面内容放进去：
```
deb http://deb.debian.org/debian/ bookworm main contrib non-free
deb-src http://deb.debian.org/debian/ bookworm main contrib non-free
```

保存并退出
```bash
sudo apt-get update
```
再次尝试安装：
```bash
sudo apt-get install libatlas-base-dev
```