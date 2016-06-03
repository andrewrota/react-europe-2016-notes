React Redux Analytics by [Evan Schultz](https://twitter.com/e_p82) and [Berrand Karenangabo](https://twitter.com/codenarian)

Build, Measure, Learn

Measuring is hard, and we aren't very good at it.

Scattered instrumentation code: Some of it is conde, some of it lives in the DOM.  You have to cover different execution paths.  There's low cohesion, you must attempt to measure hte same semantic event all over the codebase.  And historically analytics has been tied to templates (e.g., `data-event` attrs).

Scale across teams and releases: large systems are difficult to understand and reason about, measuring them even more so.

in redux, middleware can act as a place for side effects in your system. e.g, here you can add your analytics into the redux loop.  so analytics can be declarative, and we have access to the entire application state.  colocate the thing we're measuring with the actual measurements, as opposed to some other abstraction of that interaction (e.g., with dom nodes).
