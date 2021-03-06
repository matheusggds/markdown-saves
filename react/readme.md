# React 

Basically is a resume for [Maximilian Schwarzmüller - React Course](https://www.udemy.com/react-the-complete-guide-incl-redux/), which you should buy, because is awesome.

## Components

### Statefull vs Stateless

#### Statefull Components / Container
- Is when your component is managing with state. 
- Since React 16.8, stateful is not automatically a class-based component, its a components that manages state, as class-based os using React Hooks.


#### Stateless Components / Presentational
- It is a functional component that does not manage state

OBS: the question of course is why and the answer is by splitting your app into container components which
is another term for these components that manage the state in your app and the dumb presentational components,
by making that split, you keep your app manageable because you have a predictable flow of data, you know
where your state changes, that will be in a couple of components and the other components are only there
to render a nice user interface and they only define on external inputs, on props and that simply ensures
that these components are highly predictable, that you can throw them anywhere into your application
and they work if you pass the right inputs in and as your application grows, you therefore have an easier
time maintaining it.

So having a lot of dumb or presentational components is a good idea.

### Class-based vs Functional Components

...

### Component Lifecycle

- it's only available in class-based components.

> You will actually learn that functional components when using React hooks have an equivalent you could say but generally, it's only available in class-based components.

Methods:
- constructor()
- getDerivedStateFromProps()
- getSnapshotBeforeUpdate()
- componentDidCatch()
- componentWillUmount()
- shouldComponentUpdate()
- componentDidUpdate()
- componentDidMount()
- render()

#### Component Lifecycle - Creation

-- component lifecycle creation image --

1. *constructor*: You can do it for basic initialization work, for example for setting an initial state.
What you shouldn't do here is cause side effects.
Now the word side effect is relatively abstract,
in the end it means things like sending a HTTP request or storing something in your local storage of the
browser or sending some analytics to Google analytics.
You don't really want to do things like that in the constructor because that can impact performance and
cause unnecessary re-render cycles which of course are pretty bad and you want to avoid.

2. *getDerivedStateFromProps*: you'll not use that lifecycle hook a lot but if you have some scenario where props of your component can change and then you want to update some internal state of that component, then
this is the hook to use and I will show you how that hook works as well. *Don't cause side effect either

3. *render*: You should use it only to prepare the data as you need it to lay out your JSX code and to render the
HTML code so to say. What you still shouldn't do in there is send HTTP requests or set any timeouts,so nothing which can block this rendering process.

> Now when render runs and you do render any other React components in this class-based component, then these child components will now be rendered. So every child component you included in your rendered component here will then be rendered as well and only once all child components were rendered and that their lifecycle looks finished, your lifecycle hook here will finish for the creation when componentDidMount gets called

4. *componentDidMount*: Here, you can cause side effects. You shouldnt update the state here synchronously.

#### Component Lifecycle - Update

-- component lifecycle update image --

1. _getDerivedStateFromProps(props, state)_: you'll not use too often, you would use it to initialize the state of a component that updates base on props you're getting.

2. _shouldComponentUpdate(nextProps, nextState)_: Here you can decide whether or not React should coninute evaluating and re-rendering the component. For performance optimization...

3. _render()_: Now after that, the render method is called and React then goes through the JSX code, evaluates that and basically constructs its virtual DOM into which I'll also dive later in this module for you and sees if it needs to update the real DOM. 

> Update Child Component Props

4. _getSnapshotBeforeUpdate(prevProps, prevState)_: This is a lifecycle hook that takes the previous props and the previous state as input and that actually returns a snapshot object which you can freely configure and this also is a niche lifecycle hook which we'll not use too much, you use it for last minute DOM operations but with that, I don't really mean changes to the DOM but things like getting the current scrolling position of the user.

5. _componentDidUpdtate_

#### useEffect() in Functional Components

We have to import it from React and it's called useEffect. useEffect is the second most important React hook you can use next to useState because useEffect and now that sounds strange but useEffect basically combines the functionality or the use cases you can cover of all these class-based lifecycle hooks in one React hook here and both is called hook,it's actually not related.This is not a lifecycle hook,this is a React hook so basically a function you can add into one of your functional components.

If you know when you want your function to run, you should add a second argumento to your `useEffect()` passing what data changes is responsable for this code to rund. Ex.:

``` javascript
useEffect(() => {
    console.log(`oi`);

    setTimeOut({
        alert('Saved data to cloud!');
    }, 1000);
}, [props.data])
```

*So now this effect should only executed when our `props.data` changed.


So if you just need componentDidMount, you would use useEffect with an empty array passed as a second argument to the useEffect function. If you have a dependency on a certain field, you do what we did before, you pass that field in here and of course, you can have multiple fields you will depend on.

``` javascript
useEffect(() => {
    console.log(`oi`);

    setTimeOut({
        alert('Saved data to cloud!');
    }, 1000);
}, [])
```
*now this will work as componentDidMount

#### Cleaning up with Lifecycles Hooks & useEffect()
If you want to cleanup some event listeners you set up somehwere, anything like that, any cleanup work you want to do.

In a class-based component you can add `componentWillUnmount()` and on useEffect you should return a function while useEffect second argument is a empty array.

#### shouldComponentUpdate()

Check here to update this component only when the props it uses is really different from before. It saves a lot of performance at re-rendering a component event when it doesnt really changed.

Re-rendering is not necessary a DOM Re-render, but Virtual DOM re-render.

``` javascript
shouldComponentUpdate(nextProps, nextState) {
    if (nextProps.data !== this.props.persons) {
        return true;
    } else {
        return false;
    }
}
```
*careful with reference types here

#### Optmize performance of Functional Component

- React.memo()
This basically uses memoization which is a technique where React will memorize, so basically store a snapshot of this component and only if its input changes, it will re-render it and otherwise if its inputs do not change and some parent component wants to update this component.

``` javascript
import React from 'react';

const persons = () => {
    return (
        <h1>jsx content</h1>
    )
}

export default React.memo(persons);
```

### Pure Component
Pure component in the end is just a normal component that already implements shouldComponentUpdate with a complete props check, so that checks for any changes in any prop of that component.

So if that is what you need, you can also just use pure component instead of manually implementing this shouldComponentUpdate check. The result will be the same, so you can do either of these but of course you can save some code if you use pure component.

``` javascript
import React, { PureComponent } from 'react';

class Persons extends PureComponent {}
```

At _functional components_ you can use [React.memo](https://pt-br.reactjs.org/docs/react-api.html#reactmemo)

### How React Updates The DOM

The render method being called does not immediately also render this to the real DOM.

The name can be misleading, this does not mean that it renders it to the DOM. Render is more a suggestion of what the HTML should look like in the end but render can very well be called and lead to the same result as is already displayed and that is part of the reason why we use shouldComponentUpdate to prevent unnecessary render calls.

Re-rendering or calling render doesn't immediately update the real DOM, instead React makes a comparison. It compares the old virtual DOM to the new one and it checks if there are any differences.

If it can detect differences, it reaches out to the real DOM and updates it and even then, it doesn't re-render the real DOM entirely, it only changes it in the places where differences were detected,

-- how react updated the dom image --

### Rendering adjacents JSX elements

React does allow us to return an array of adjacent elements as long as all the items in there have a key and that key is required so that React can efficiently update and reorder these elements as it might be required by your app.

### HOC - High Order Components
HOC is a function that accepts a component as parameter and return a augmented version of this original component.

You can do thing like:
- Messing with the original past props inspecting them or even changing them
- Rendering something else entirely instead of rendering the original component

They are basically components that wrap other components and in there.

> It's kind of a convention to name higher order components with a with at the beginning, though of course

For example:

Create a HOC `WithClass.js`, witch returns a wrapper element using _classes_ passed by props.

``` javascript
import React from 'react';

const withClass = props => (
    <div className={props.classes}>
        {props.children}
    </div>
)

export default withClass;

```

and usage:

``` javascript
import WithClass from 'withClassPath';

<WithClass classes="active">
    <h1>Title</h1>
    <p>content content</p>
</WithClass>
```

Obviously there would be nothing wrong with sticking to a div but we'll introduce other higher order components where we for example add error handling that we can wrap around any component that makes an HTTP request and all of a sudden, this becomes more useful.

### Setting state correctly when depending on the old state
Set state does not only take a Javascript object, it also works when you pass in a function, so you can use either syntax.

Now when you're doing state updates that don't depend on the old state, there is nothing wrong with just passing the object.

``` javascript
this.setState((prevState, props) => {
    return {
        counter: prevState.counter + 1
    }
})
```

### Proptypes
Is a NPM pkg to easly indicate which and what props your component will receive.

`npm i --save prop-types` to use it.

``` javascript
import { PropTypes } from 'prop-types';

yourComponent.propTypes = {
    click: PropTypes.func,
    name: PropTypes.string,
    age: PropTypes.number
}
```

### Refs
Ref, just like key, is a special property you can pass into any component, it is detected and understood by React.

One way to use Refs:
``` javascript
componentDidMount() {
    this.inputElement.focus();
}

<component
    onChange={this.props.func}
    ref={(inputEl) => {this.inputElement = inputEl}}
/>
```

Another approach, newer, is using [React.createref](https://pt-br.reactjs.org/docs/refs-and-the-dom.html)

At _functional components_ you can use [useRef()](https://pt-br.reactjs.org/docs/hooks-reference.html#useref)

### Context API / Props chain problems

Context was introduced by React and it helps us handle cases like, where you need certain data, certain state in multiple components and you don't want to pass that state across multiple layers of components just to get it from component A at the top to component D at the very bottom when the components B, C in between don't really care about it and that's exactly the use case here.

We want to skip parent component and with the React context feature, we can do that.

#### Using context API

[Context API](https://pt-br.reactjs.org/docs/context.html)

Let`s imagine a context which handle authentication data.

Create a `context` folder and create a file called `auth-context.js`.

_auth-context.js_
``` javascript
import React from 'react';

const authContext = React.createContext({
    authenticated: false
})

export default authContext;
```

Now React create context actually allows us to initialize our context with a default value because what the context in the end is is a globally available Javascript object you could say, though globally available is not entirely correct, you decide where it is available. But it is a Javascript object that can be passed between React components without using props, behind the scenes so to say

_app.js_
``` javascript
import AuthContext from 'filePath';

<AuthContext.Provider>
    ... Component which use authContext context
</AuthContext.Provider>
```

So in there, let's import AuthContext with a capital A at the beginning from the context folder and there of course the auth-context file. Now authContext can be used as a component and it should wrap and that's important, it should wrap all the parts of your application that need access to this context.

_This section must be completed... Sorry_

## Planning a React App

- **Component Tree / Component Structure**:  You probably got a design by your designer or you basically created an app design on your own and now it's up to you to split this up into React components and it's absolutely normal that the result you may have at the end might look different than your initially planned component tree but it's super important to have an idea about what should go into its own component and what not.

- **Application state**: You can also translate this with the data you plan on using and manipulating in your application

- **Components vs Containers**: So which components in your application should be stateless, also sometimes called dumb components, so basically components that are functional and don't use hooks or even class-based components that don't use state and which components have to be stateful components, so either functional components using their useState hook or class-based components using the state property.

----
We are use a Burger Builder project as example.

### Layout and Component Tree
We need to define what our application actually is and what it should be able to do. 

So the goal is that users can use this app to add ingredients and therefore build a burger. 

_layout_

_component tree_

_burger builder component_

### Planning State
we also need to know which state we're going to use in our application. 

This state becomes important because it also allows us to identify what should be a component and what should be a container. So what should be a stateless component and what should be a stateful component.

_burger planning state_