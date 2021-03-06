---
title: React.js
category: React
layout: 2017/sheet
ads: true
tags: [Featured]
updated: 2017-09-01
weight: -10
---

{%raw%}

Components
----------
{: .-three-column}

### Components
{: .-prime}

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
```
{: .-setup}

```jsx
class Hello extends React.Component {
  render () {
    return <div className='message-box'>
      Hello {this.props.name}
    </div>
  }
}
```

```jsx
const el = document.body
ReactDOM.render(<Hello name='John' />, el)
```

Use the [React.js jsfiddle](http://jsfiddle.net/reactjs/69z2wepo/) to start hacking. (or the unofficial [jsbin](http://jsbin.com/yafixat/edit?js,output))

### Properties

```html
<Video fullscreen={true} />
```
{: .-setup}

```jsx
render () {
  this.props.fullscreen
  ···
}
```
{: data-line="2"}

Use `this.props` to access properties passed to the component.
See: [Properties](https://facebook.github.io/react/docs/tutorial.html#using-props)

### States

```jsx
this.setState({ username: 'rstacruz' })
```

```jsx
render () {
  this.state.username
  ···
}
```
{: data-line="2"}

Use states (`this.state`) to manage dynamic data.
See: [States](https://facebook.github.io/react/docs/tutorial.html#reactive-state)

### Nesting

```jsx
class Info extends React.Component {
  render () {
    const { avatar, username } = this.props

    return <div>
      <UserAvatar src={avatar} />
      <UserProfile username={username} />
    </div>
  }
}
```
{: data-line="6,7"}

Nest components to separate concerns. See: [Composing Components](https://facebook.github.io/react/docs/components-and-props.html#composing-components)


### Children

```jsx
<AlertBox>
  <h1>You have pending notifications</h1>
</AlertBox>
```
{: data-line="2"}

```jsx
class AlertBox extends React.Component {
  render () {
    return <div className='alert-box'>
      {this.props.children}
    </div>
  }
}
```
{: data-line="4"}

Children are passed as the `children` property.

Defaults
--------

### Setting default props

```jsx
Hello.defaultProps = {
  color: 'blue'
}
```
{: data-line="1"}

See: [defaultProps](https://facebook.github.io/react/docs/react-component.html#defaultprops)

### Setting default state

```jsx
class Hello extends React.Component {
  constructor (props) {
    super(props)
    this.state = { visible: true }
  }
}
```
{: data-line="4"}

Set the default state in the `constructor()`.

Other components
----------------
{: .-three-column}

### Function components

```jsx
function MyComponent ({ name }) {
  return <div className='message-box'>
    Hello {name}
  </div>
}
```
{: data-line="1"}

Functional components have no state. Also, their `props` are passed as the first parameter to a function.
See: [Function and Class Components](https://facebook.github.io/react/docs/components-and-props.html#functional-and-class-components)

### Pure components

```jsx
class MessageBox extends React.PureComponent {
  ···
}
```
{: data-line="1"}

Performance-optimized version of `React.Component`. Doesn't rerender if props/state hasn't changed.
See: [Pure components](https://facebook.github.io/react/docs/react-api.html#react.purecomponent)

### Component API

```jsx
this.forceUpdate()
```

```jsx
this.setState({ ... })
```

```jsx
this.state
this.props
```

These methods and properies are available for `Component` instances. See: [Component API](http://facebook.github.io/react/docs/component-api.html)

Lifecycle
---------
{: .-two-column}

### Mounting

| Method | Description |
| --- | --- |
| `constructor` _(props)_ | Before rendering [#](https://facebook.github.io/react/docs/react-component.html#constructor) |
| `componentWillMount()` | _Don't use this_ [#](https://facebook.github.io/react/docs/react-component.html#componentwillmount) |
| `render()` | Render  [#](https://facebook.github.io/react/docs/react-component.html#render) |
| `componentDidMount()` | After rendering (DOM available) [#](https://facebook.github.io/react/docs/react-component.html#componentdidmount) |
| --- | --- |
| `componentWillUnmount()` | Before DOM removal [#](https://facebook.github.io/react/docs/react-component.html#componentwillunmount) |

Set initial the state on `constructor()`.
Add DOM event handlers, timers (etc) on `componentDidMount()`, then remove them on `componentWillUnmount()`.

### Updating

| Method | Description |
| --- | --- |
| `componentWillReceiveProps` *(newProps)* | Use `setState()` here |
| `shouldComponentUpdate` *(newProps, newState)* | Skips `render()` if returns false |
| `componentWillUpdate` *(newProps, newState)* | Can't use `setState()` here |
| `render()` | Render |
| `componentDidUpdate` *(prevProps, prevState)* | Operate on the DOM here |

Called when parents change properties and `.setState()`. These are not called for initial renders. See: [Reference](http://facebook.github.io/react/docs/component-specs.html#updating-componentwillreceiveprops).

DOM nodes
---------
{: .-two-column}

### References

```jsx
class MyComponent extends React.Component {
  render () {
    return <div>
      <input ref={el => this.input = el} />
    </div>
  }

  componentDidMount () {
    this.input.focus()
  }
}
```
{: data-line="4,9"}

Allows access to DOM nodes. See: [Refs and the DOM](https://facebook.github.io/react/docs/refs-and-the-dom.html)

### DOM Events

```jsx
class MyComponent extends React.Component {
  render () {
    <input type="text"
        value={this.state.value}
        onChange={event => this.onChange(event)} />
  }

  onChange (event) {
    this.setState({ value: event.target.vlaue })
  }
}
```
{: data-line="5,9"}

Pass functions to attributes like `onChange`. See: [Events](https://facebook.github.io/react/docs/events.html)

## Other features

### Transfering props

```html
<VideoPlayer src="video.mp4" />
```
{: .-setup}

```jsx
class VideoPlayer extends React.Component {
  render () {
    return <VideoEmbed {...this.props} />
  }
}
```
{: data-line="3"}

Propagates `src="..."` down to the sub-component.
See [Transferring props](http://facebook.github.io/react/docs/transferring-props.html).

### Top-level API

```jsx
React.createClass({ ... })
React.isValidElement(c)
```

```jsx
ReactDOM.render(<Component />, domnode, [callback])
ReactDOM.unmountComponentAtNode(domnode)
```

```jsx
ReactDOMServer.renderToString(<Component />)
ReactDOMServer.renderToStaticMarkup(<Component />)
```

There are more, but these are most common.
See: [React top-level API](https://facebook.github.io/react/docs/react-api.html)

JSX patterns
------------
{: .-two-column}

### Style shorthand

```jsx
var style = { height: 10 }
return <div style={style}></div>
```

```jsx
return <div style={{ margin: 0, padding: 0 }}></div>
```

See: [Inline styles](https://facebook.github.io/react/tips/inline-styles.html)

### Inner HTML

```jsx
function markdownify() { return "<p>...</p>"; }
<div dangerouslySetInnerHTML={{__html: markdownify()}} />
```

See: [Dangerously set innerHTML](https://facebook.github.io/react/tips/dangerously-set-inner-html.html)

### Lists

```jsx
class TodoList extends React.Component {
  render () {
    const { items } = this.props

    return <ul>
      {items.map(item =>
        <TodoItem item={item} key={item.key} />)}
    </ul>
  }
}
```
{: data-line="6,7"}

Always supply a `key` property.

### Conditionals

```jsx
<div>
  {showPopup
    ? <Popup />
    : null}
</div>
```

Property validation
-------------------
{: .-three-column}

### PropTypes

```js
import PropTypes from 'prop-types'
```
{: .-setup}

See: [Typechecking with PropTypes](https://facebook.github.io/react/docs/typechecking-with-proptypes.html)

| PropType                  | Description                          |
| ---                       | ---                                  |
| `any`                     | Anything                             |
| ---                       | ---                                  |
| `string`                  |                                      |
| `number`                  |                                      |
| `func`                    | Function                             |
| `bool`                    | True or false                        |
| ---                       | ---                                  |
| `oneOf`_(any)_            | Enum types                           |
| `oneOfType`_(type array)_ | Union                                |
| ---                       | ---                                  |
| `array`                   |                                      |
| `arrayOf`_(...)_          |                                      |
| ---                       | ---                                  |
| `object`                  |                                      |
| `objectOf`_(...)_         | Object with values of a certain type |
| `instanceOf`_(...)_       | Instance of a class                  |
| `shape`_(...)_            |                                      |
| ---                       | ---                                  |
| `element`                 | React element                        |
| `node`                    | DOM node                             |
| ---                       | ---                                  |
| `.isRequired`             | Required                             |

### Basic types

```jsx
MyComponent.propTypes = {
  email:      PropTypes.string,
  seats:      PropTypes.number,
  callback:   PropTypes.func,
  isClosed:   PropTypes.bool,
  any:        PropTypes.any
}
```

### Required types

```jsx
MyCo.propTypes = {
  name:  PropTypes.string.isRequired
}
```

### Elements

```jsx
MyCo.propTypes = {
  // React element
  element: PropTypes.element,

  // num, string, element, or an array of those
  node: PropTypes.node
}
```

### Enumerables (oneOf)

```jsx
MyCo.propTypes = {
  direction: PropTypes.oneOf([
    'left', 'right'
  ])
}
```

### Arrays and objects

```jsx
MyCo.propTypes = {
  list: PropTypes.array,
  ages: PropTypes.arrayOf(PropTypes.number),
  user: PropTypes.object,
  user: PropTypes.objectOf(PropTypes.number),
  message: PropTypes.instanceOf(Message)
}
```

```jsx
MyCo.propTypes = {
  user: PropTypes.shape({
    name: PropTypes.string,
    age:  PropTypes.number
  })
}
```

Use `.array[Of]`, `.object[Of]`, `.instanceOf`, `.shape`.

### Custom validation

```jsx
MyCo.propTypes = {
  customProp: (props, key, componentName) => {
    if (!/matchme/.test(props[key])) {
      return new Error('Validation failed!')
    }
  }
}
```

Also see
--------
{: .-one-column}

* This reference was made for React v15.
* [React v0.14 cheatsheet](react@0.14) _Legacy version_
* [React website](http://facebook.github.io/react) _facebook.github.io_
{:.-also-see}

{%endraw%}
