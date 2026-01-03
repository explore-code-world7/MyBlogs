# 挂在设置权限
```bash
sudo umount  /dev/sdb1
sudo mount -o rw,uid=1000,gid=1000,iocharset=utf8 /dev/sdb1 /media/sky/SSD
```

# 新解压工具

```bash
sudo apt install bsdtar  # 安装
bsdtar -xf ShapeNetCore.v1.zip -C /path/to/ spacious_target/
```
