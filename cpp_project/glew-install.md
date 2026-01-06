# ubuntu20.04

1. 下载glew2.2.0.zip

github.com/nigels-com/glew/releases

2. 在目录下make，不要用auto下的make

3. `sudo make install`

4. 创建符号链接

```bash
sudo ln -sf /usr/lib64/libGLEW.so.2.2.0 /usr/lib/x86_64-linux-gnu/libGLEW.so.2.2
```

# 服务器没屏幕

```bash
ShapeNetCore.v2/04256520/10552f968486cd0ad138a53ab0d038a5/models/model_normalized.obj --> data/SdfSamples/ShapeNetV2/04256520/10552f968486cd0ad138a53ab0d038a5.npz
terminate called after throwing an instance of 'std::runtime_error'
  what():  Pangolin X11: Failed to open X display
```

* solution
```bash
sudo apt update && sudo apt install xvfb
xvfb-run -a python preprocess_data.py --data_dir data --source data/ShapeNetCore.v2/ --name ShapeNetV2 --split examples/splits/sv2_sofas_train.json --skip
```
