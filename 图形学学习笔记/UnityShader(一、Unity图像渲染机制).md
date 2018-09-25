本文转自：
[https://www.jianshu.com/p/1d7becd48210](https://www.jianshu.com/p/1d7becd48210 "https://www.jianshu.com/p/1d7becd48210")，请点击链接查看原文，尊重楼主版权。

# Unity图像渲染机制 #

在Unity引擎中，任何图像渲染都需要一个很重要的文件属性——Material（材质球），在MeshRenderer、LineRenderer、UI渲染、拖尾渲染都可以见到它的影子。因此，我们可以将Material理解为Unity中图像渲染的工具，而Shader（着色器）即可以理解为Material这个工具的加工厂，Shader（加工厂）定义了Material渲染的解决方案，定义了Material渲染所需要的原材料，而此时所讲的原材料，即Shader中的属性（数值，颜色，纹理，贴图等等）。

![Unity图像渲染机制](https://i.imgur.com/h4Ar4W4.png)

下面举例说明，在Unity中设置一个网格渲染的具体流程：
	
- 想要渲染一个网格，首先需要创建一个材质球

	![创建材质球](https://i.imgur.com/tYP3ltk.png)

- 在材质球中，选择合适的Shader

	![选择Shader](https://i.imgur.com/7vG6iah.png)

- 将材质球添加到网格渲染器中

	![添加材质球到网格渲染器](https://i.imgur.com/9qxtT72.png)

- 调整材质球中的属性信息

	![调整材质属性](https://i.imgur.com/0nD203t.png)

- 查看调整后的渲染效果

	![查看渲染效果](https://i.imgur.com/WMiN80s.png)