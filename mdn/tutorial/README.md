### webgl
WebGL程序包括用 JavaScript 写的控制代码，以及在图形处理单元（GPU, Graphics Processing Unit）中执行的着色代码（GLSL，注：GLSL为OpenGL着色语言）

[WebGL仅仅是一个光栅化引擎，它可以根据你的代码绘制出点，线和三角形。](https://webglfundamentals.org/webgl/lessons/zh_cn/webgl-fundamentals.html)

drawing a square and we're putting it directly in front of the camera perpendicular to the view direction. 

### The shaders 着色器
A shader is a program, written using the [OpenGL ES Shading Language (GLSL)](https://www.khronos.org/files/opengles_shading_language.pdf), that takes information about the vertices that make up a shape and generates the data needed to render the pixels onto the screen: namely, ***the positions of the pixels and their colors***.  

#### 两种 着色器函数
the vertex shader 顶点着色器  
the fragment shader 片段着色器  
通过用GLSL 编写这些着色器，并将代码文本传递给WebGL ， 使之在GPU执行时编译  
顶点着色器和片段着色器的集合我们通常称之为着色器程序  

### 顶点着色器
每次渲染一个形状时，顶点着色器会在形状中的每个顶点运行  
它的工作是将输入顶点从原始坐标系转换到WebGL使用的缩放空间([clip space](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_model_view_projection#Clip_space))坐标系，其中每个轴的坐标范围从-1.0到1.0，并且不考虑*纵横比*，*实际尺寸*或任何其他因素。  
将其保存在由GLSL提供的特殊变量（我们称为gl_Position）中来返回变换后的顶点  

[texel(texture pixel)](https://en.wikipedia.org/wiki/texel_(graphics)) [varyings](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Data#Varyings) [attributes](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Data#Attributes)

### 片段着色器
顶点着色器处理完图形的顶点后，会被要绘制的**每个图形的每个像素点**调用一次。它的职责是确定像素的颜色，通过指定应用到像素的纹理元素（也就是图形纹理中的像素），获取纹理元素的颜色，然后将适当的光照应用于颜色。之后颜色存储在特殊变量gl_FragColor中，返回到WebGL层。该颜色将最终绘制到屏幕上图形对应像素的对应位置。

### BUFFER
```
const colors = [
    1.0, 1.0, 1.0, 1.0,    // white
    1.0, 0.0, 0.0, 1.0,    // red
    0.0, 1.0, 0.0, 1.0,    // green
    0.0, 0.0, 1.0, 1.0,    // blue
];
const colorBuffer = gl.createBuffer();
gl.bindBuffer(gl.ARRAY_BUFFER, colorBuffer);
gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(colors), gl.STATIC_DRAW);
```