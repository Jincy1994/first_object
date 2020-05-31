## Flux（架构思想）
- View：试图层
- AcionCreator（动作创造者）： 试图层发出的信息（比如mouseClick）
- Dispatcher（派发器）：用来接收Actions，执行回掉函数 
- Store（数据层）： 用来存放应用的状态，一旦发生变动，就提示views更行页面
## Flux的流程
1. 组件获取到store中保存的数据挂载在自己的状态上
2. 用户生产了操作，调用ations的方法
3. actions接收到了用户的操作，进行一系列的逻辑代码，异步操作
4. 然后actions会创建出对应的ation，action带有标识性的属性
5. actions调用dispatcher的dispatch方法将ation传递给dispatcher
6. dispatcher接收到action并根据标识信息判断之后，调用store的更改数据的方法
7. store的方法被调用后，更改状态，并出发自己的某一个事件
8. store更改状态后事件被触发，该事件的处理程序会通知view去获取最新的数据