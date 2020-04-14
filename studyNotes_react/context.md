# context
## context说明：
- context提供了一个无需为每层组件手动添加props，就能在组件树间进行数据传递的方法。
## context的使用：
1. 引入context
```javascript
import React.{ Component, createContext } from 'react'
```
2. context解构
```javascript
const {
    Provider,
    Consumer: CounterConsumer
} = createContext()
```