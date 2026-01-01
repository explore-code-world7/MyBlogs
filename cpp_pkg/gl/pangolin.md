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

# Data Sturcture
除了 `pangolin::Image`，Pangolin 还定义了以下基本数据结构：

## 图像和像素相关

### `Point` / `ImageDim`
2D点坐标结构，包含 x 和 y 成员 [1](#4-0) 

### `ImageRoi`
图像区域结构，定义矩形的 x, y, w, h 参数 [2](#4-1) 

### `PixelFormat`
像素格式描述，包含格式字符串、通道数、位深度等信息 [3](#4-2) 

### `TypedImage`
带像素格式信息的图像，继承自 `ManagedImage<unsigned char>` [4](#4-3) 

## 几何和图形相关

### `Geometry`
几何体结构，包含 buffers、objects、textures 等组件 [5](#4-4) 

### `Colour`
OpenGL 颜色表示，包含 RGBA 浮点值 [6](#4-5) 

### `GlTexture`
OpenGL 纹理包装器，提供纹理上传、下载和渲染功能 [7](#4-6) 

## 变量和数据管理

### `VarMeta`
变量元数据，包含名称、范围、增量、标志等信息 [8](#4-7) 

### `VarValueGeneric`
变量值的抽象基类，用于类型擦除的变量管理 [9](#4-8) 

### `DataLog` / `DataLogBlock`
数据记录结构，用于时间序列数据的存储和统计 [10](#4-9) 

## 设备和视频相关

### `Guid`
64位设备唯一标识符 [11](#4-10) 

### `FirewireFrame`
火线相机帧结构，包含图像数据和时间戳信息 [12](#4-11) 

## Notes

这些数据结构体现了 Pangolin 作为图形和视频处理库的设计理念：
- **通用性**：如 `Image` 可用于存储任意2D数据
- **类型安全**：通过模板和继承提供类型化的数据容器
- **OpenGL集成**：如 `GlTexture` 直接映射到OpenGL资源
- **跨平台**：统一的接口抽象不同平台的硬件设备

每个结构都针对特定的使用场景优化，共同构成了Pangolin的核心数据模型。

***

# Geomety: 天生mesh描述
`pangolin::Geometry` 是一个用于表示3D几何体的结构体，包含顶点数据、面片索引和纹理信息。

## 成员变量

### `buffers`
存储顶点属性数据的映射表，键为缓冲区名称，值为 `Element` 类型 [1](#5-0) 。

### `objects` 
存储索引缓冲区的多重映射表，键为对象名称，值为 `Element` 类型 [2](#5-1) 。

### `textures`
存储纹理图像的映射表，键为纹理名称，值为 `TypedImage` 类型 [3](#5-2) 。

## 嵌套结构 `Element`

### 继承关系
继承自 `ManagedImage<uint8_t>`，提供内存管理功能 [4](#5-3) 。

### `attributes`
存储属性数据的映射表，使用 `std::variant` 支持多种图像类型：
- `Image<float>` - 浮点数据（如顶点坐标、法线）
- `Image<uint32_t>` - 32位整数（如顶点索引）
- `Image<uint16_t>` - 16位整数
- `Image<uint8_t>` - 8位整数 [5](#5-4) 

## 相关函数

### `LoadGeometry(filename)`
从文件加载几何体，支持 OBJ 和 PLY 格式 [6](#5-5) 。

### `GetAxisAlignedBox(geom)`
计算几何体的轴对齐包围盒（需要 Eigen 支持） [7](#5-6) 。

## Notes

`Geometry` 结构体采用分层设计：
- **buffers** 存储顶点数据（位置、法线、颜色、纹理坐标等）
- **objects** 存储面片索引，定义如何连接顶点形成几何形状
- **textures** 存储材质贴图

这种设计支持复杂的3D模型，包括多个子对象和纹理。实际使用中，通常通过 `LoadGeometry()` 从文件加载，然后访问相应的属性数据进行渲染或处理。

