# js模块化规范
## CommonJs
### 说明：
- 每一个文件都可当作一个模块
- 在服务器端模块的加载是运行时同步加载的
- 在浏览器端模块需要提前编译打包处理
### 基本语法
> 暴露模块
> - module.exports = value
> - exports.xxx = value
> - 暴露的模块到底是什么：是exports对象

> 引入模块
>> require(xxx)
>> - 第三方模块xxx为模块名
>> - 自定义模块xxx为模块文件路径
### 实现
> 服务器端实现：node.js

> 浏览器端实现：`Browserify`（也成为commonjs的浏览器端的打包工具，因为浏览器端的是已经编译好的)
>> - `dist`：打包生成文件的目录，`srcs`：源码所在的目录
>> - 下载`Browserify`：全局安装还要在局部安装
>>>   - 全局安装：`npm install browserify -g`
>>>   - 局部安装：`npm install browserify --save-dev`
>> - 打包处理js：
>>> - breowserify js/src/app.js -o js/dist/bundle.js (-o是output的意思)


## AMD
## CMD（理解就可以）
## ES6
### 说明：依赖模块需要打包处理
### 语法：
- 导出模块：exprot
  - 分别暴露
  > exprot function foo(){}
  - 统一暴露
  > export {fun1,fun2}//把两个函数放进对象里统一暴露，还有这个写法是es6的对象简写方式
  - `以上两种暴露方式在引入的时候要求必须使用解构赋值的形式import {xxx} from‘路径’`
  - 默认暴露：可以暴露任意数据类型，暴露什么数据接收到的就是什么数据
  > export default xxx;接收时不用解构接收
- 引入模块：import
  - import xxx from‘路径’
  - 引入第三方库：import xxx from '包名'
### 实现
- 使用Babel将ES6编译为ES5代码
- 使用打包工具（Browserify）进行编译打包
> 操作
>> 安装babel-cli，babel-preset-es2015，和browserify（cli：command line interface，就是命令行）
>> - npm install babel-cli browserify -g
>> - npm install babel-preset-es2015 --save-dev
>> - preset 预设（将es6转换成es5的所有插件打包）

>> 定义 `.babelrc`文件(与packagejson同等级目录
>>> - babel的插件工作之前先会去读这个配置文件
>>> - {"presets": ["es2015"]}告诉babel的插件要干什么，要转换成es5的语法
>>> - `rc`文件的意思:run control,运行时控制文件，就是运行时需要读的文件
### 编译
- 使用babel将es6编译为es5代码（但包含commonjs语法，也就是编译出来的模块语法是commonjs的语法所以需要再用browserify进行编译）：babel js/src -d js/lib
