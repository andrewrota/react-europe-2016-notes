Recomposing your React Application by [Andrew Clark](https://twitter.com/acdlite)

Deep dive on higher order components.

Higher order component is `(component) => component` a component that takes a component and returns a component.

Example: `const ComponentWithRouter = withRouter(Component)`

How do HOCs work?  Higher order components work by secretly wrapping the input component inside a container component.

Review: container vs. presentational component.  A pattern in react where some components are designed to be purely presentational, and then other components do more complex tasks such as managing subscriptions, data fetching, etc.  And these are called container componets.  Sometimes called dumb and smart components.

HOCs work by composing the original component.

HOCs are parameterized container components.

Use cases and trade-offs

Start with the presentational components when implementing a use case in react.  This is a good approach because it forces you to think about the contracts in the components.  Then you add the container components.  Say you want some mock data to work on with your presentational component.  So you could use a `withProps({data})(Component)` HOC.

Small utility HOCs can be composed into more useful HOCs.

downsides might be another developer understanding your code.

Created library called [recompose](https://github.com/acdlite/recompose) with a library of useful HOCs:

* `mapProps`
* `mapPropsSteam` (in rx-recopmose currently): compose together the transformations and then pass htem to mapPropsStream which means it only results in a single component: `mapPropsStream(compose(transform1, transform2, transform3)`.
* 
