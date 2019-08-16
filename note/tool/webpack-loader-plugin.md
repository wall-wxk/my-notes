# webpack loader 和 plugin 解析

## 构建流程

webpack的运行过程可以简单概述为如下流程：

初始化配置参数 -> 绑定事件钩子回调 -> 确定Entry逐一遍历 -> 使用loader编译文件 -> 输出文件

- 首先，webpack会读取你在命令行传入的配置以及项目里的 webpack.config.js 文件，初始化本次构建的配置参数，并且执行配置文件中的插件实例化语句，生成Compiler传入plugin的apply方法，为webpack事件流挂上自定义钩子。
- 接下来到了entryOption阶段，webpack开始读取配置的Entries，递归遍历所有的入口文件
- Webpack进入其中一个入口文件，开始compilation过程。先使用用户配置好的loader对文件内容进行编译（buildModule），我们可以从传入事件回调的compilation上拿到module的resource（资源路径）、loaders（经过的loaders）等信息；之后，再将编译好的文件内容使用acorn解析生成AST静态语法树（normalModuleLoader），分析文件的依赖关系逐个拉取依赖模块并重复上述过程，最后将所有模块中的require语法替换成__webpack_require__来模拟模块化操作。
- emit阶段，所有文件的编译及转化都已经完成，包含了最终输出的资源，我们可以在传入事件回调的compilation.assets 上拿到所需数据，其中包括即将输出的资源、代码块Chunk等等信息


介于node.js单线程的壁垒，webpack构建慢一直成为它饱受诟病的原因。

## loader

```javascript
module.exports = function(content){
    //return "{};" + content
    this.callback(null, "{};" + content)
}
```

这些loader的执行顺序是从后往前的，你也可以把它理解为这个loaders数组的出栈过程。
在默认情况下，webpack会对loader的执行结果进行缓存，这样能够大幅度提升构建速度

## pitch钩子

pitch 的函数，它会先于所有的loader执行。
它可以接受三个参数，最重要的就是第三个参数data，你可以为其挂在一些所需的值，一个rule里的所有的loader在执行时都能拿到这个值。

```javascript
module.exports = function(content){
    //***this data*** test
    console.log('***this data***', this.data.value)
    return "{};" + content
}

module.exports.pitch = (remaining, preceding, data) => {
    data.value = "test"
}
```

## plugin

```javascript
//@file: plugins/myplugin.js
class myPlugin {
    constructor(options){
        //用户自定义配置
        this.options = options
        console.log(this.options)
    }
    apply(compiler) {
        console.log("This is my first plugin.")
    }
}

module.exports = myPlugin
```