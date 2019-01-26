react의 state를 잘못사용하는 경우와 올바르게 사용하는 경우 비교

```javascript
// Wrong
this.state.comment = 'Hello';
// Correct
this.setState({comment: 'Hello'});
--------------------------------------
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

setState는 비동기 함수