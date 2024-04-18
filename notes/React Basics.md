### Virtual DOM
- The virtual DOM (VDOM) is a programming concept where an ideal, or “virtual”, representation of a UI is kept in memory and synced with the “real” DOM by a library such as ReactDOM. This process is called [reconciliation](https://legacy.reactjs.org/docs/reconciliation.html).

- Virtual DOM is an ideal representation of UI that is kept in memory. Once any update is made to the virtual DOM it is synced with the real DOM to show it on the screen.

- The process of updating is followed like this:
    - The update is passed to the virtual DOM.
    - Virtual DOM checks if anything is actually updated by comparing the current virtual DOM and the pre-updated virtual DOM before updating the real DOM. This process is called diffing.
    - If anything was actually updated then the real DOM is synced with the virtual DOM. Here syncing will update only those parts of the DOM that have been updated in the virtual DOM rather than updating the whole DOM.

---
### Is the Shadow DOM the same as the Virtual DOM?

No, they are different. The Shadow DOM is a browser technology designed primarily for scoping variables and CSS in web components. The virtual DOM is a concept implemented by libraries in JavaScript on top of browser APIs.

### What is “React Fiber”?

Fiber is the new reconciliation engine in React 16. Its main goal is to enable incremental rendering of the virtual DOM. [Read more](https://github.com/acdlite/react-fiber-architecture).

## Components
A react application can be visualized like a tree. Each node in the tree is a component that renders some JSX. It is compulsory for components to return some JSX; it can’t return undefined.

Components help in making JSX code reusable and independent of where it is being rendered. In components, we use something known as props which means some data that has been passed from the parent to the child component. See the example below for a reference.

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
function App(props) {
  return <Welcome name="John Doe">;
}
```

# State: A Component's Memory
We can use regular variables in React however there’s a problem with storing vital data in regular variables as this data can be lost between re-renders; therefore we need to store vital data in a way that the data is not lost between re-renders.

This is where states come into play. States are special kinds of storage spaces that store the data and this data cannot be lost between re-renders. States created using the useState hook can be set only using their corresponding state setters. In class-based components, the state can only be set using this.setState function.

States will hold the data from the mounting of the component till the component unmounts or in other words, the state of a component will be maintained throughout the component’s life cycle.
```jsx
import { useState } from 'react';
import { sculptureList } from './data.js';

export default function Gallery() {
  const [index, setIndex] = useState(0);

  function handleClick() {
    setIndex(index + 1);
  }

  let sculpture = sculptureList[index];
  return (
    <>
      <button onClick={handleClick}>
        Next
      </button>
      <h2>
        <i>{sculpture.name} </i> 
        by {sculpture.artist}
      </h2>
      <h3>  
        ({index + 1} of {sculptureList.length})
      </h3>
      <img 
        src={sculpture.url} 
        alt={sculpture.alt}
      />
      <p>
        {sculpture.description}
      </p>
    </>
  );
}

```

>**Hooks—functions starting with `use`—can only be called at the top level of your components or [your own Hooks.](https://react.dev/learn/reusing-logic-with-custom-hooks)** You can’t call Hooks inside conditions, loops, or other nested functions. Hooks are functions, but it’s helpful to think of them as unconditional declarations about your component’s needs. You “use” React features at the top of your component similar to how you “import” modules at the top of your file.

### Anatomy of `useState` [](https://react.dev/learn/state-a-components-memory#anatomy-of-usestate "Link for this heading")

When you call [`useState`](https://react.dev/reference/react/useState), you are telling React that you want this component to remember something:

```
const [index, setIndex] = useState(0);
```

![[Pasted image 20240417081740.png]]

Each component goes through the same life cycle regardless of the type of component it is i.e. functional or class-based components. The only thing that differs between functional components and class-based components is the life cycle methods.

When a component first mounts the function componentDidMount (class-based function) or useEffect with an empty dependency array (functional component) is invoked.

- ComponentDidUpdate is invoked when either a state or a prop is updated. useEffect with that specific prop or state in the dependency array is invoked.
- componentWillUnmount is called just before unmounting. This functional component is handled by useEffect with an empty dependency array with a return function at the end of the useEffect.
- The return part of useEffect and componentWillUnmount should be used to clean up before applying new effects to the component.
- Read more about State and Lifecycle [here](https://reactjs.org/docs/state-and-lifecycle.html).

## Event propagation [](https://react.dev/learn/responding-to-events#event-propagation "Link for Event propagation")

Event handlers will also catch events from any children your component might have. We say that an event “bubbles” or “propagates” up the tree: it starts with where the event happened, and then goes up the tree.

This `<div>` contains two buttons. Both the `<div>` _and_ each button have their own `onClick` handlers. Which handlers do you think will fire when you click a button?
# Event Handling

Events in HTML are also used in React. The only difference is their naming is different in React. Events in React are written in camelcase. Say – onclick becomes onClick.

```jsx
<button onclick="activate()"> activate </button>
```
Becomes

```jsx
<button onClick={activate}> activate </button>
```
### Stopping propagation [](https://react.dev/learn/responding-to-events#stopping-propagation "Link for Stopping propagation")

Event handlers receive an **event object** as their only argument. By convention, it’s usually called `e`, which stands for “event”. You can use this object to read information about the event.

That event object also lets you stop the propagation. If you want to prevent an event from reaching parent components, you need to call `e.stopPropagation()` like this `Button` component does:
```jsx
function Button({ onClick, children }) {
  return (
    <button onClick={e => {
      e.stopPropagation();
      onClick();
    }}>
      {children}
    </button>
  );
}

export default function Toolbar() {
  return (
    <div className="Toolbar" onClick={() => {
      alert('You clicked on the toolbar!');
    }}>
      <Button onClick={() => alert('Playing!')}>
        Play Movie
      </Button>
      <Button onClick={() => alert('Uploading!')}>
        Upload Image
      </Button>
    </div>
  );
}

```
#### Capture phase events 
In rare cases, you might need to catch all events on child elements, _even if they stopped propagation_. For example, maybe you want to log every click to analytics, regardless of the propagation logic. You can do this by adding `Capture` at the end of the event name:

```jsx
<div onClickCapture={() => { /* this runs first */ }}>  
	<button onClick={e => e.stopPropagation()} /> 
	<button onClick={e => e.stopPropagation()} />  
</div>
```

### Preventing default behavior 
`e.stopPropagation()` and `e.preventDefault()`. They are both useful, but are unrelated:

- [`e.stopPropagation()`](https://developer.mozilla.org/docs/Web/API/Event/stopPropagation) stops the event handlers attached to the tags above from firing.
- [`e.preventDefault()`](https://developer.mozilla.org/docs/Web/API/Event/preventDefault) prevents the default browser behavior for the few events that have it.