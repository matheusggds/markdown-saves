# React 

Basically is a resume for [Maximilian Schwarzmüller - React Course](https://www.udemy.com/react-the-complete-guide-incl-redux/), which you should buy, because is awesome.

## Definition

React could be defined by a Library to build web interfaces. A lot of people get it confused by a Framework but isn't. A Framework has a lot of functionalities like Angular, Vue, etc.

It is focused on Components. The rest is made by other libraries like Redux, Router, etc.

## Components

#### Statefull vs Stateless

##### Statefull Components / Container
- Is when your component is managing with state. 
- Since React 16.8, stateful is not automatically a class-based component, its a components that manages state, as class-based os using React Hooks.


##### Stateless Components / Presentational
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

#### Class-based vs Functional Components

...

#### Component Lifecycle

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

##### Component Lifecycle - Creation

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

##### Component Lifecycle - Update

-- component lifecycle update image --

1. _getDerivedStateFromProps(props, state)_: you'll not use too often, you would use it to initialize the state of a component that updates base on props you're getting.

2. _shouldComponentUpdate(nextProps, nextState)_: Here you can decide whether or not React should coninute evaluating and re-rendering the component. For performance optimization...

3. _render()_: Now after that, the render method is called and React then goes through the JSX code, evaluates that and basically constructs its virtual DOM into which I'll also dive later in this module for you and sees if it needs to update the real DOM. 

> Update Child Component Props

4. _getSnapshotBeforeUpdate(prevProps, prevState)_: This is a lifecycle hook that takes the previous props and the previous state as input and that actually returns a snapshot object which you can freely configure and this also is a niche lifecycle hook which we'll not use too much, you use it for last minute DOM operations but with that, I don't really mean changes to the DOM but things like getting the current scrolling position of the user.

5. _componentDidUpdtate_

##### useEffect() in Functional Components

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

If you need the *component unmount* lifecycle, just return a function inside your effect like:

``` javascript
useEffect(() => {
  window.addEventListener('resize', () => handleMobile())
  
  return () => {
    window.removeEventListener('resize', () => handleMobile())
  }
}, [])
```
