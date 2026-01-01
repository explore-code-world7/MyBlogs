* Pangolin是一个窗口管理类
* 采用和OPENGL类似的形式，渲染image和video,



# 对OpenGL的基础类进行封装
* 以GlTexture为例

| 特性     | OpenGL 原生             | Pangolin `GlTexture`       |
| ------ | --------------------- | -------------------------- |
| 类型     | `GLuint`              | 类 `pangolin::GlTexture`    |
| 生命周期管理 | 手动 `glDeleteTextures` | 析构自动释放                     |
| 绑定     | `glBindTexture`       | 成员函数 `Bind()` / `Unbind()` |
| 数据上传   | `glTexImage2D`        | 内部封装 `Upload()`            |
| 功能扩展   | 仅纹理句柄                 | 支持数组纹理、3D纹理、mipmap 等封装     |

* Pangolin GlTexture 不是 OpenGL 原生纹理对象，而是 封装类。
* 内部 确实使用了 OpenGL 的纹理对象 (GLuint)。
* 优势：RAII 管理、简化绑定/上传操作、支持多种纹理类型。
* 如果你需要直接操作 OpenGL 纹理，也可以拿到 GLuint 句柄。

## 从pangolin获取原生textureID
```cpp
GLuint texID = texVideo.texture_id;
```

***

