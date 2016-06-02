Keynote by [Dan Abramov](https://twitter.com/dan_abramov)

Redux: state management library often used with react, but also popular

mobile twitter is now using redux

What made redux successful?  Redux doesn't have many features.  It's just a change emitter holding a single value.  The implementation is simple.  People aren't choosing redux because of its features and APIs...because there are no features.  Don't think of libraries purely in terms of their features and APIs.

A building architect might think of architecture as interior and exterior.  But as they become more experienced they realize the value of architecture is the space in the building for people to work in.

People choose redux because of constraints and contracts rather than Features and APIs.

Redux constraints:

* Single State Tree
* Actions Describe Updates
* Reducers Apply Updates

Debug workflow:

* Log actions and states
* Find the bad state
* Check the action
* Fix the reducer
* Write a test (it's easy to test reducers since they're pure functions)

Everything is data:

* Persistence
* Universal rendering
* Recording user sessions
* Optimistic mutations
* Collaborative editing (actions are already plain objects so they can be passed through the network)

Constraints are just as important as features.  Constraints give you some features in return.

Redux contracts that the user implements:

* Reducers
* Selectors
* Middleware
* Enhancers

Group reducers and selectors

Higher order reducers: `(reducer, ...args) => reducer`

* redux-optimistic-ui
* react-redux-form (wrapers model reudcer but enhances it with the fields tracking the clean/dirty values of form)

Middleware:

* redux-observable
* redux-logger
* apollo-client

Enhances:

* redux-batched-subscribe
* redux-loop (elm architecture in js)
* redux-devtools-extension (devtools in remote client)

Contracts need to be designed as carefully as APIs.

"Make contracts social...composable"

Design the way out (use redux contracts even if you're not using redux)

Find the useful stress tests.

Understanding matters.  Provide a good understanding of what's happening in your library.

Other libraries to look at: relay, rxjs, mobx

Future of redux: small stepping stone to immutable app architecture. See Lee Byron's talk at RenderConf 2016.  On how immutable architecture can deliver great ux and dx.

Cohesive story:

* Declarative data fetching
* Built-in optimistic mutations
* Easy-to-test async control flow
* Combining local and server data
* Great developer experience

Redux started as an experiment, and it's still an experiment.

new set of redux tutorials: egghead.io/redux-2


