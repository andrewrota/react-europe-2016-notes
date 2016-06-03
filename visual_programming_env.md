Evolving the Visual Programming Environment with React by [Jonas Gebhardt](https://twitter.com/jonasgebhardt)

project called 'combine'

but engineers already know how to code, and it's so much more powerful.  but code is just another tool.

alternative representation can be useful to determine how data flows through an app.

direct manipulation is a lot easier because you know where to put things.

TTP: time to product.  this is the metric for a lot of people in the room.  no matter your process it's all about time.

prototyping has been around for a while as a solution to TTP problems.  as the fidelity of your prototype grows, so does the cost.

the existing visual editors are platform-specific, and they have tiny ecosystems and lack network effects. and have limited UX.

package manager wishlist

* versioned
* properly namespaced
* statically typed interfaces
* semantically annotated and documented
* bonus: quality indicators from usage data

why isn't there a yelp for packages yet?

brief note on static typing

turns out flow can be compiled to js, so adding static types here adds new possibilities.

in combine, the node represents a runnable.  optional react component on every node that encapsulates all of its side effects.

pure functions are referentially transparent, which means you could replace the fn call with its output value.

but side effects have to be somehwere, because otherwise you wouldn't have UI, IO, time, randomness.  So we need good abstractions to handle these explicitly.  Here, they're handled in optional components for performing side effects.  the engine takes care of storing the global state.  separating the side effects from the implementation is powerful.

observables are the async glue of this.  observables are collections that arrive over time. both sync and async computation can be represented as observables.

with the editor you are literally interacting with the data as it flows

the engine: takes the state of the editor and recomposes the implementation graph.  chains together the pure functions with the observable async glue.  maintains DAG of composed nodes.  on change, reconciles composition of runnable implementations with config in editor.  only necessary work gets re-computed.

apps = components + layouts

we can pull out just the side effect encapsulating component and re-arrange them and out comes an app.

every node has a static type interface, so we could all of a sudden build equivalent components.

this is just a prototype, but it's a model for interacting with data and computation and it's worth thinking about how we can make tooling better.