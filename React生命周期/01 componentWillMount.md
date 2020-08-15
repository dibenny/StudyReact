1.  ## componentWillMount

`UNSAFE_componentWillMount()`

```
⚠️ 注意:该方法即将过时，请谨慎使用
该生命周期以前称为componentWillMount。该名称将一直使用到版本17。
<rename-unsafe-lifecycles codemod>自动更新您的组件。
```

- `UNSAFE_componentWillMount()`在挂载发生之前被调用。在之前 render()调用，因此 setState()在此方法中同步调用不会触发额外的呈现。通常，我们建议使用 constructor()代替初始化状态。

在 componentWillMount 中执行 this.setState 是不会触发二次渲染的。

它也只会在挂载过程中被调用一次，它的作用和 constructor 没有太大差异。有很多人在 componentWillMount 中请求后台数据，认为这样可以更早的得到数据，componentWillMout 是在 render 函数执行前执行的，虽然请求是在第一次 render 之前发送的，但是返回并不能保证在 render 之前完成。render 不会等你慢慢请求.所以在渲染的时候没有办法等到数据到来再去 setState 触发二次渲染.

仔细思考一下，componentWillMount 好像没啥卵用了。正所谓存在即合理，在服务端渲染的场景中 componentDidMount 是不会被执行的，因此可以在 componnetWillMount 中发生 AJAX 请求。

顺便说一句在 es6 中,使用 extend component 的方式里的 constructor 函数和 componentWillMount 是通用的作用,所以你在构造函数里初始化了组件的状态就不必在 WillMount 做重复的事情了.

React 中不推荐在 componentWillMount 中发送异步请求。

2. ## componentDidMount

- `componentDidMount()`会在组件挂载后（插入 DOM 树中）立即调用。依赖于 DOM 节点的初始化应该放在这里。如需通过网络请求获取数据，此处是实例化请求的好地方。

componentDidMount 这个生命周期函数在是在 render 之后调用一次,component 已经初始化完成了.

在生产时,componentDidMount 生命周期函数是最好的时间去请求数据,其中最重要原因:使用 componentDidMount 第一个好处就是这个一定是在组件初始化完成之后,再会请求数据,因此不会报什么警告或者错误,我们正常请教数据完成之后一般都会 setStat

3. ## componentWillReceiveProps()

`UNSAFE_componentWillReceiveProps(nextProps)`

```
⚠️ 注意:该方法即将过时，请谨慎使用
此生命周期之前名为 componentWillReceiveProps。该名称将继续使用至 React 17。
<rename-unsafe-lifecycles codemod>自动更新您的组件
```

会在已挂载的组件接收新的 props 之前被调用。如果你需要更新状态以响应 prop 更改（例如，重置它），你可以比较 this.props 和 nextProps 并在此方法中使用 this.setState() 执行 state 转换。

请注意，如果父组件导致组件重新渲染，即使 props 没有更改，也会调用此方法。如果只想处理更改，请确保进行当前值与变更值的比较。

在挂载过程中，React 不会针对初始 props 调用 UNSAFE_componentWillReceiveProps()。组件只会在组件的 props 更新时调用此方法。调用 this.setState() 通常不会触发 UNSAFE_componentWillReceiveProps()。
