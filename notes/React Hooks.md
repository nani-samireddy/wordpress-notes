Hooks are the functions that let you use states without needing to return anything or without needing to write a class. Using hooks comes with some rules as hooks cannot be used conditionally because it leads to inconsistent behavior.

Hooks are functions that allow you to hook into React lifecycle. Also remember, that hooks cannot be used in class-based components

## useState
useState is a hook that returns a state variable and a state setter. The state is initialized with the argument passed to the useState hook.
```jsx
const [count, setCount] = useState(0);
```

# useEffect
useEffect is a hook that is used to perform some side-effects in a component like a network calls, or subscribing to an event.

- useEffect is a combination of componentWillUpdate, componentWillUnmount and componentDidMount. It is of two types: one without a cleanup function and another with a cleanup function.
    - Cleanup functions are recommended in useEffect so that we can stop memory leaks. Clean-up functions are run before applying new effects to the component. They are similar to componentWillUnmount.
- There can be multiple useEffect in a single component where each useEffect can focus on different things. useEffect comes with a dependency array which means the useEffect will only run if the variable in the dependency array changes.
- Usage of useEffect:
```jsx
useEffect(() => {   function handleStatusChange(status) {     setIsOnline(status.isOnline);   }   ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);   return () => {  ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);   }; }, [props.friend.id]);
```
## 1. The infinite loop and side-effect updating state
Let's say you want to create a component having an input field, and also display how many times the user changed that input.

Here's a possible implementation of `<CountInputChanges>` component:
```jsx
import { useEffect, useState } from 'react';

function CountInputChanges() {
  const [value, setValue] = useState('');
  const [count, setCount] = useState(-1);

  useEffect(() => setCount(count + 1));

  const onChange = ({ target }) => setValue(target.value);

  return (
    <div>
      <input type="text" value={value} onChange={onChange} />
      <div>Number of changes: {count}</div>
    </div>
  )
}
```
![[Pasted image 20240417162956.png]]
