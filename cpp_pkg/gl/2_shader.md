着色=把3D 坐标转为屏幕上2D带颜色点;

着色器在 GLSL(OpenGL Shading Language)中;

分为若干阶段: 
##
vertex shader:
1. transform 3D coordinates into different 3D coordinates (more on that later) ;
2. allows us to do some basic processing on the vertex attributes.

* vertex先发送到GPU上的VBO(vertex buffer objects)
### 为VBO分配 ID
```cpp
unsigned int VBO;
glGenBuffers(1, &VBO);  
```

### BufferBind: 任何buffer call作用于binded buffer
* VBO的buffer类型=GL_ARRAY_BUFFER
```cpp
glBindBuffer(GL_ARRAY_BUFFER, VBO);  
```
### data>buffer
* GL_STATIC_DEAW = the graphics card to manage the given data

```cpp
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
```

## 
fragment shader
1. generate other shapes by emitting new vertices to form new (or other) primitive(s).
2. assembles all the vertices (or vertex if GL_POINTS is chosen) from the vertex (or geometry) shader that form one or more primitives in the primitive shape given;


## 
rasterization
1. maps the resulting primitive(s) to the corresponding pixels on the final screen, resulting in fragments for the fragment shader to use.
2. clipping is performed Before discards all fragments that are outside your view, increasing performance.

>  A fragment in OpenGL is all the data required for OpenGL to render a single pixel.

