# **渲染管线-应用阶段**

参考自：Unity Shader入门精要，本文为本人 学习笔记，请读者尊重原著版权，多多支持冯乐乐前辈的著作。

渲染流水线的起点是CPU，即应用阶段。该阶段大致可分为以下3个阶段：

### **1.把数据加载到显存中**

所有渲染所需的数据都需要**从硬盘(HDD)中加载到系统内存(RAM)中**，然后，**网格和纹理等数据又被加载到显卡上的存储空间--显存(VRAM)中**。
这是因为：显卡对于显存的访问速度更快，而且大多数显卡对于RAM没有直接的访问权利。
例：
![](https://i.imgur.com/YiYBgnZ.png)

**注**：真实渲染需要加载到显存中的数据往往比上图复杂多，例如：顶点的法线位置信息、法线方向、顶点颜色、纹理坐标等。

当把数据加载到显存中后，RAM中的数据就可以移除了。但对于一些数据来说，CPU仍需要访问他们(例如，我们希望CPU可以访问网格数据来进行碰撞检测），那么我们可能就不希望这些数据被移除，因为从硬盘加载到RAM的过程是十分耗时的。

### **2.设置渲染状态**
渲染状态：这些状态定义了场景中的网格是怎样被渲染的。
例如：使用哪个顶点着色器/片元着色器、光源属性、材质等。

如果我们没有更改渲染状态，那么所有的网格都将使用同一种渲染状态。
下图显示了当使用同一渲染状态时，渲染3个不同网格的结果。

![](https://i.imgur.com/kwaDdMa.png)

准备好这些以后，CPU就需要调用一个渲染命令--DrawCall来告诉GPU，数据已经准备好，可以按照设置开始渲染了。

### **3.调用Draw Call**
Draw Call就是一个命令，发起方是CPU，接收方是GPU。
这个命令**仅仅会指向一个需要被渲染的图元列表，而不会再包含任何材质信息**--因为我们已经在上一阶段完成了。(渲染图元可以是点、线、三角面等)
过程如下图：
![](https://i.imgur.com/y4JxdPx.png)

当给定一个Draw Call时，就会进入下一节的GPU流水线：
GPU就会进入根据渲染状态(例如材质、纹理、着色器等)和所有输入的顶点数据来进行计算，最终输出成屏幕上显示的那些漂亮的像素。