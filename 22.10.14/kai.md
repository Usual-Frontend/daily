# React组件化开发

## 一.函数式组件与类组件

- 函数式组件不需要继承，类组件需要继承
- 函数式组件与类组件的首字母都需要大写
- 类组件通过render函数返回，而函数组件直接return

## 二.类组件的常用生命周期函数

- **constructor()** 构造方法；每次创建的实例都会先执行这个函数，通常用于绑定this和初始化state
- **render()** 渲染；再执行render方法渲染
- **componentDidMount()** 被挂载到DOM，依赖DOM的操作可以在这里进行，可以发送ajax请求
- **componentDidUpdate()** DOM发生更新;首先执行render函数，再执行当前函数
- **componentWillUnmount() **DOM被移除时执行

## 三.组件之间的通信

### 1.父子组件通信

- 父组件

  ```jsx
  <MyComponent 属性=值></MyComponent>
  <MyComponent key={value}></MyComponent>
  //传递对象的时候可以直接用...来传递
  <MyComponent {...Object}></MyComponent>
  ```

- 子组件

  ```jsx
  class Son extends React.component {
      //通过props来接受父组件传过来的值
      constructor(props){
          //将props保存到实例里
          super(props)
      }
      render(){
          return this.props.key  //渲染展示数据
      }
  }
  ```

### 2.prop类型验证

- 利用prop-types库来进行类型验证

  ```jsx
  //父组件
  <MyComponent key={value}></MyComponent>
  //子组件验证
  import propTypes from 'prop-types'
  MyComponent.propTypes = {
      //是数组并且必须传入
      key:propsTypes.array.isRequired
  }
  MyComponent.defaultProps = {
      //传入默认值
      key:'value'
  }
  ```

### 3.子父组件通信

- 父组件

  ```jsx
  //直接传入一个函数，子组件利用props接受这个函数
  <MyComponent functionName={() => {}}></MyComponent>
  ```

- 子组件

  ```jsx
  //通过this.props.functionName拿到函数
  this.props.fn() //拿到函数并调用
  ```

## 四.插槽实现方式

### 1.通过组件的children子元素来实现

- 父组件

  ```jsx
  <MyComponent>
      //直接传入
  	<button>按钮</button>
      <div>文本</div>
  </MyComponent>
  ```

- 子组件

  ```jsx
  //通过this.props.children拿到传递过来的元素，并用数组方式排列。只有一个不是数组
  <div>{this.props.children[0]}</div> //展示按钮button
  <div>{this.props.children[1]}</div> //展示文本div
  ```

### 2.通过props传递React元素

- 父组件

```jsx
//通过key=value方式传递
<MyComponent left={<button>buttton</button>} right={<div>文本</div>}>
</MyComponent>
```

- 子组件

```jsx
<div>{this.props.left}</div> //展示按钮button
<div>{this.props.right}</div> //展示文本div
```

## 