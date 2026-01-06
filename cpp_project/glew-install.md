# ubuntu20.04

1. 下载glew2.2.0.zip

github.com/nigels-com/glew/releases

2. 在目录下make，不要用auto下的make

3. `sudo make install`

4. 创建符号链接

```bash
sudo ln -sf /usr/lib64/libGLEW.so.2.2.0 /usr/lib/x86_64-linux-gnu/libGLEW.so.2.2
```
