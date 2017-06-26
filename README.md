# Что нужно знать при работе с REACT

1 - подключаем библиотеку REACT:
```javascript
  import React, { Component } from 'react'
  import React, { PureComponent } from 'react'
```
`PureComponent` будет всегда заново отрисовывать компоненты, если будет получать ссылки на разные объекты в `props` и `state`. Он предполагает неглубокую проверку, что сокращает количество рендеров в приложении.

главный компонент:
```javascript
  import React from 'react';	
```
2 - создаем класс, если нужно хранить значения в `state`
```javascript
  class App extends Component { // || PureComponent
    constructor(props) {
      super(props)
    }
  }
```
  Если `state` не нужен, то создаем `stateless` ф-цию
```javascript
  const MyComponent = (props) => {
    return (
      // JSX
    )
  }
```
`props` - свойства компонента, передаются как атрибуты

3 - храним состояние
```javascript
  this.state = { value: '' };
```
или
```javascript
  getInitialState() {
    return { value: '' }    
  }
```
4 - валидация переменных при помощи библиотеки `prop-types`
```javascript
  <Class Name>.propTypes =  {
    value(то что this.props.value): React.PropTypes.string.isRequired,  // для цифр
    onColorChange: React.PropTypes.func	   // для функции
  }
```
5 - если нужно взаимодействие с браузером (срабатывает только при инициализации)
```javascript
  componentDidMount() {...}
```
6 - изменение переменно хранящейся в `state`
```javascript
  this.setState({
    value: this.state.value + 1,        // для переменной
    arr: this.state.arr.concat([...])  // для массива
  });  
```
`this.state`,`this.props` - обновляються асинхронно!
#### Лучше передать в `setState` функцию, а не объект
```javascript
  this.setState((prevState, props) => (
    {value: prevState.value + 1}
  ));
```
7 - Информацию об элементе можно получить c помощью `ref`
```javascript
  <... ref="city">  получаем this.refs.city
```
Атрибут `ref` принимает функцию обратного вызова, и вызывает ее после того, как компонент монтируется в `DOM` или удаляется из него. Использовал для фокуса в `input`:
```javascript
  <input
    type="text"
    ref={(input) => { this.textInput = input }}
  />
```
8 - отрисовка компонента
```javascript
  render() {
    return (...)
  }
```
отрисовка главного компанента:
```javascript
  ReactDOM.render( <App />, document.getElementById('root'));		
```
9 - передаваемая функция в props, вызывается в компоненте-конструктор с параметрами компонента-конструктора и в компоненте их получаем в аргументе

  Компонент-конструктор
```javascript
  <input onChange={(e)=>props.onValue(e, e.target.value)} />
```

  Компонент
```javascript		
  <input onValue={(e, value) => value} />
```	

10 - обратиться к `NODE` элементам, рекомендуется только в `componentDidMount()` и `componentWillUnmount()` в `constructor()` все узлы добавляемые через `REACT` равны `undefined`, т.к. срабатывает раньше прорисовки `DOM` дерева
