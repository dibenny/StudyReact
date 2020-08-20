1.  ## UNSAFE_componentWillMount()

`UNSAFE_componentWillMount()`

⚠️ 注意:该方法即将过时，请谨慎使用
该生命周期以前称为 `componentWillMount。`该名称将一直使用到版本 17。

- `UNSAFE_componentWillMount()`在挂载发生之前被调用。在之前 `render()`调用，因此 setState()在此方法中同步调用不会触发额外的呈现。通常，我们建议使用 `constructor()`代替初始化状态。

在 `componentWillMount` 中执行 `this.setState` 是不会触发二次渲染的。

它也只会在挂载过程中被调用一次，它的作用和 `constructor`没有太大差异。有很多人在 `componentWillMount`中请求后台数据，认为这样可以更早的得到数据，`componentWillMout`是在 `render` 函数执行前执行的，虽然请求是在第一次 `render`之前发送的，但是返回并不能保证在 `render` 之前完成。render 不会等你慢慢请求.所以在渲染的时候没有办法等到数据到来再去 setState 触发二次渲染.

仔细思考一下，`componentWillMount` 好像没啥卵用了。正所谓存在即合理，在服务端渲染的场景中 `componentDidMount` 是不会被执行的，因此可以在`componnetWillMount`中发生 AJAX 请求。

顺便说一句在 es6 中,使用 `extend component`的方式里的 `constructor` 函数和 `componentWillMount` 是通用的作用,所以你在构造函数里初始化了组件的状态就不必在 WillMount 做重复的事情了.

React 中不推荐在 `componentWillMount` 中发送异步请求。

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  componentWillMount() {
    // change code below this line

    // change code above this line
  }
  render() {
    return <div />
  }
};
```

2. ## componentDidMount

- `componentDidMount()`会在组件挂载后（插入 DOM 树中）立即调用。依赖于 DOM 节点的初始化应该放在这里。如需通过网络请求获取数据，此处是实例化请求的好地方。

`componentDidMount`这个生命周期函数在是在 render 之后调用一次,`component` 已经初始化完成了.

在生产时,`componentDidMount` 生命周期函数是最好的时间去请求数据,其中最重要原因:使用 c`omponentDidMount`第一个好处就是这个一定是在组件初始化完成之后,再会请求数据,因此不会报什么警告或者错误,我们正常请教数据完成之后一般都会`setStat`

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      activeUsers: null
    };
  }
  componentDidMount() {
    setTimeout( () => {
      this.setState({
        activeUsers: 1273
      });
    }, 2500);
  }
  render() {
    return (
      <div>
        <h1>Active Users: { /* change code here */ }</h1>
      </div>
    );
  }
};
```

3. ## componentWillReceiveProps()

`UNSAFE_componentWillReceiveProps(nextProps)`

⚠️ 注意:该方法即将过时，请谨慎使用
此生命周期之前名为`componentWillReceiveProps`。该名称将继续使用至 React 17。

会在已挂载的组件接收新的`props` 之前被调用。如果你需要更新状态以响应 `prop` 更改（例如，重置它），你可以比较 `this.props` 和 `nextProps` 并在此方法中使用`this.setState()` 执行`state`转换。

请注意，如果父组件导致组件重新渲染，即使 props 没有更改，也会调用此方法。如果只想处理更改，请确保进行当前值与变更值的比较。

在挂载过程中，React 不会针对初始 props 调用 `UNSAFE_componentWillReceiveProps()`。组件只会在组件的 `props`更新时调用此方法。调用 `this.setState()` 通常不会触发 `UNSAFE_componentWillReceiveProps()`。

4. ## shouldComponentUpdate()

`shouldComponentUpdate(nextProps, nextState)`

到目前为止，如果任何组件接收到新的`state`或新的`props`，它会重新渲染自己及其所有子组件。这通常是好的。但是 `React`提供了一种生命周期方法，当子组件接收到新的 state 或 props 时，你可以调用该方法，并特别声明组件是否应该更新。方法是`shouldComponentUpdate()`，它将`nextProps`和`nextState`作为参数。

这种方法是优化性能的有效方法。例如，默认行为是，当组件接收到新的`props`时，即使`props`没有改变，它也会重新渲染。你可以通过使用`shouldComponentUpdate()`比较`props`来防止这种情况。该方法必须返回一个布尔值，该值告诉 `React` 是否更新组件。你可以比较当前的`props（this.props）`和下一个 `props（nextProps）`，以确定你是否需要更新，并相应地返回`true`或`false`。

⚠️ 注意:
如果 shouldComponentUpdate() 返回 false，则不会调用 UNSAFE_componentWillUpdate()

根据 `shouldComponentUpdate()` 的返回值，判断 `React` 组件的输出是否受当前`state`或 `props`更改的影响。默认行为是 `state` 每次发生变化组件都会重新渲染。大部分情况下，你应该遵循默认行为。

当 `props`或 `state` 发生变化时，`shouldComponentUpdate()` 会在渲染执行之前被调用。返回值默认为 `true`。首次渲染或使用 `forceUpdate()` 时不会调用该方法。

我们不建议在 `shouldComponentUpdate()` 中进行深层比较或使用 `JSON.stringify()`。这样非常影响效率，且会损害性能。

```
class OnlyEvens extends React.Component {
  constructor(props) {
    super(props);
  }
  shouldComponentUpdate(nextProps, nextState) {
    console.log('我需要更新吗?');
     // change code below this line
    return true;
     // change code above this line
  }
  componentWillReceiveProps(nextProps) {
    console.log('接受新的props...');
  }
  componentDidUpdate() {
    console.log('组件已重新渲染.');
  }
  render() {
    return <h1>{this.props.value}</h1>
  }
};

class Controller extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 0
    };
    this.addValue = this.addValue.bind(this);
  }
  addValue() {
    this.setState({
      value: this.state.value + 1
    });
  }
  render() {
    return (
      <div>
        <button onClick={this.addValue}>Add</button>
        <OnlyEvens value={this.state.value}/>
      </div>
    );
  }
};
```

运行结果

```
// tests completed
接受新的props...
我需要更新吗?
组件已重新渲染.
接受新的props...
我需要更新吗?
组件已重新渲染.
```

5. ## UNSAFE_componentWillUpdate

`UNSAFE_componentWillUpdate(nextProps, nextState)`

⚠️ 注意

此生命周期之前名为 `componentWillUpdate`。该名称将继续使用至 React 17

当组件收到新的 `props` 或 `state` 时，会在渲染之前调用 `UNSAFE_componentWillUpdate()`。使用此作为在更新发生之前执行准备更新的机会。初始渲染不会调用此方法。

注意，你不能此方法中调用 `this.setState()；`在 `UNSAFE_componentWillUpdate()` 返回之前，你也不应该执行任何其他操作（例如，dispatch Redux 的 action）触发对 React 组件的更新

通常，此方法可以替换为 `componentDidUpdate()`。如果你在此方法中读取 DOM 信息（例如，为了保存滚动位置），则可以将此逻辑移至 `getSnapshotBeforeUpdate()` 中。

⚠️ 注意

如果 `shouldComponentUpdate()` 返回 false，则不会调用 `UNSAFE_componentWillUpdate()`

6. ## componentDidUpdate()

`componentDidUpdate(prevProps, prevState, snapshot)`

`componentDidUpdate()` 会在更新后会被立即调用。首次渲染不会执行此方法。

当组件更新后，可以在此处对 DOM 进行操作。如果你对更新前后的 props 进行了比较，也可以选择在此处进行网络请求。（例如，当 props 未发生变化时，则不会执行网络请求）。

```
componentDidUpdate(prevProps) {
  // 典型用法（不要忘记比较 props）：
  if (this.props.userID !== prevProps.userID) {
    this.fetchData(this.props.userID);
  }
}
```

⚠️ 注意

如果 `shouldComponentUpdate()`返回值为 false，则不会调用 `componentDidUpdate()`。

7. ## componentWillUnmount()

`componentWillUnmount()`

`componentWillUnmount()`会在组件卸载及销毁之前直接调用。在此方法中执行必要的清理操作,

`componentWillUnmount()`中不应调用 `setState()`，因为该组件将永远不会重新渲染。组件实例卸载后，将永远不会再挂载它。
