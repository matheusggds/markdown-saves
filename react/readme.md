# React 

Basically is a resume for [Maximilian Schwarzmüller - React Course](https://www.udemy.com/react-the-complete-guide-incl-redux/), which you should buy, because is awesome.

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

#### Component Lifecycle

- it's only available in class-based components.
` *You will actually learn that functional components when using React hooks have an equivalent you could say but generally, it's only available in class-based components. `

Methods
- constructor(): You can do it for basic initialization work, for example for setting an initial state.
What you shouldn't do here is cause side effects.
Now the word side effect is relatively abstract,
in the end it means things like sending a HTTP request or storing something in your local storage of the
browser or sending some analytics to Google analytics.
You don't really want to do things like that in the constructor because that can impact performance and
cause unnecessary re-render cycles which of course are pretty bad and you want to avoid.

- getDerivedStateFromProps(): you'll not use that lifecycle hook a lot but if you have some scenario where props
of your component can change and then you want to update some internal state of that component, then
this is the hook to use and I will show you how that hook works as well. *Don't cause side effect either

- getSnapshotBeforeUpdate()
- componentDidCatch()
- componentWillUmount()
- shouldComponentUpdate()
- componentDidUpdate()
- componentDidMount()
- render()
