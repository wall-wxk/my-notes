# 关键渲染路径

## 渲染路径步骤

关键渲染路径分为六步。
* 创建DOM树(Constructing the DOM Tree)
* 创建CSSOM树(Constructing the CSSOM Tree)
* 执行脚本(Running JavaScript)
* 生成渲染树(Creating the Render Tree)
* 生成布局(Generating the Layout)
* 绘制(Painting)

## CSS阻塞渲染

CSS是一种__渲染阻塞资源(render blocking resource)__，它需要完全被解析完毕之后才能进入_生成渲染树_的环节。CSS并不像HTML那样能执行部分并显示，因为CSS具有继承属性， 后面定义的样式会覆盖或者修改前面的样式。如果我们只使用样式表中部分解析好的样式，我们可能会得到错误的页面效果。所以，我们只能等待CSS完全解析之后，才能进入_关键渲染路径_的下一环节。

因为JavaScript脚本的执行必须等到CSSOM生成之后，所以说CSS也会__阻塞脚本(script blocking)__。

避免使用 CSS import

被 @import 引入的 CSS 需依赖包含其的 CSS 被下载与解析完毕才能被发现

Web Fonts（Web字体）也被视为一种阻塞渲染的资源，因为它们是通过CSS加载的


## javascript阻塞渲染

当页面解析到<script>标签，不管脚本是內联的还是外联，页面解析都会暂停，转而加载JavaScript文件（外联的话）并且执行JavaScript。

解决:
- 在<script>标签上添加async属性(脚本的加载完成后就马上执行，脚本执行时会阻塞 HTML 解析)
- 在<script>标签上添加defer属性(脚本的执行要在所有元素解析完成之后，DOMContentLoaded 事件触发之前完成, defer 仅适用于外链，规定脚本延迟执行)

