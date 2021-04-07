## Provider是react-redux提供的一个组件
```js
import React from 'react';
import { CartList } from './components'
import { Provider } from 'react-redux'
import store from './store'


class App extends React.Component {
    render() {
        return(
            <Provider store={store}>
                <CartList store={store}/>                    
            </Provider>
        )
    }
}

export default App;
```
- 一般就是直接把这个组件放在应用程序的最外层，这个组件必须有一个store属性，这个store属性的值就是俺么创建的哪个store
- 只要在最外层包裹了这个Provider，那么所有后代组件都可以使用Redux.connect做连接

## 在需要使用store的组件里倒入connect
- connect(mapStateToProps,mapDispatchToProps)(组件)
    - connect有四个参数，常用的是前面两个
    - 第一个参数mapStateToProps，作用是从store里把state注入到当前组件的props上
    - 第二个参数是mapDispatchToProps，这个主要作用是把action生成的方法注入到当前组件的props里面，相当于react的dispatch
- connect方法执行之后是一个高阶组件
```js
import React, { Component } from 'react'
import { increment, decrement} from '../../actions/cart'
import { connect } from 'react-redux'

class CartList extends Component {
    componentDidMount(){
        console.log(this.props.cartList)
        console.log(this.props.add(1))
    }
    render() {

        return (
            <table>
            </table>
        )
    }

}
const mapStateToProps = (state) => {
    return {
        cartList: state.cart
    }
}

const mapDispatchToProps = dispatch => {
    return {
        add: (id) => dispatch(increment(id)),
        resuce: (id) => dispatch(decrement(id)),
    }
}

export default connect(mapStateToProps,mapDispatchToProps)(CartList)
```
- 一般不像上面那样定义mapDispatchToProps，可以直接传入actions，如下
- 注意传入的actions必须是actionCreator创建出来的（看redux的笔记就会知道actionCreator），也就是
```js
export default connect(mapStateToProps,{ increment, decrement })(CartList)
//使用时 this.props.increment.bind(this,参数)
```