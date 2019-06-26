# React 

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

So having a lot of dumb or presentational components is a good idea.

#### Class-based vs Functional Components