# context
## context说明：
- context提供了一个无需为每层组件手动添加props，就能在组件树间进行数据传递的方法。
## context的使用：
1. 引入context
```javascript
import React.{ Component, createContext } from 'react'
```
2. context解构(里面的Provider和Consumer是组件)
```javascript
const {
    Provider,
    Consumer: CounterConsumer
} = createContext()
```
3. 程序
```javascript
import React.{ Component, createContext } from 'react'
import { render } from 'reacr-dom'

const {
    Provider,
    Consumer: CounterConsumer
} = createContext()

//封装一个基本的Provider，因为直接使用Provider不方便管理状态

class CounterProvider extends Component {
    constructor () {
        super()

        //这里的状态就是共享的，任何CounterProvider的后代组件都可以通过CounterConsumer来接受这个值
        this.state = {
            count: 100
        }
    }

    //这里的方法也会通过CounterProvider共享下去

    decrementCount = () => {
        this.setState({
            count: this.state.count - 1
        }) 

    }

    incrementCount = () => {
        this.setState({
            count: this.state.count + 1
        })       
    }
    render() {
        return {

            //使用 Provider这个组件，他必须要有一个value值，这个value里可以传递任何的数据，一般还是传递一个对象比较合理
            <Provider value={{
                count: this.state.count,
                onIncrementCount: this.incrementCount,
                onDecrementCount: this.decrementCount
                
            }}>
                {this.props.children}
            </Provider>
        }

    }

}

class Counter extends Component {
    render () {
        return {

            //使用CounterConsumer来接受
            //注意CounterConsumer的chidren一定要是方法，这个方法有以个参数，这个参数就是Provider的value
            
            <CounterConsumer>
            {
                ({ count }) => {
                    return <span>{count}</span>
                }
            }   
            </CounterConsumer>
        }
    }
}

class CountBtn extends Component {
    render () {
        return {
            <CounterConsumer>
            {
                ({ onIncrementCount, onDecrementCount }) => {
                    const handler = this.props.type === 'increment' ? onIncrementCount : onDecrementCount
                    return <button onClick={handler}>{this.props.children}</button>
                }
            }   
            </CounterConsumer>      
        }
    }
}

class App extends Component {
    render () {
        return {
            <>
                <CountBtn type="decrement">-</CountBtn>
                    <Counter />
                <CountBtn type="increment">+</CountBtn>
            </>

        }
    }
}

render {
    <CounterProvider>
        <App />
    </CounterProvider>,
    document.querySelector('#root')
}
```