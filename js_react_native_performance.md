JavaScript, React Native, and Performance by [Tadeu Zagallo](https://twitter.com/tadeuzagallo)

Performance goals: reduce memory usage, reduce startup overhead

Things to improve performance in react native:

* Lazy module initialization.  remove modules you're not using, don't wait for modules to initialize, they'll be loaded on demand.
* Smarter batching: when react came out we weren't very good at multithreading.  JS, layout, and native render are happening in their own threads, but not in parallel.  Now doing as much in parallel in posible.

JavaScript optimizations:

* Inline/lazy requires: usually requires are at the top of the file, but it will also include all its dependencies.  lazy requires move the requires to where they're actually used. The tradeoffs are that the first time it has to be tapped it might not be as responsive.
* Dead code elimination
* Optimise polyfills
* Extract babel helpers

App start was primarily JS initialization/render/fetch.  80% of startup time spent in JavaScript.  So what next?

When we're on the web we think of JS as the input that goes through the VM and we get some output.  We shape our code in terms of the VM since we know what it can optimize.  On react native, we ship the VM with the app though.  So we can actually modify the VM if we need to.

Copy code --> parse --> AST gen --> bytecode generation --> bytecode interpretation> -- baseline jit --> dfg jit --> ftl jit but then replaced with B3 which has better throughput

But, third party apps can't jit on ios.  So we're back to stage 1.  But we can jit on Android, but it's slower.

Android setup: Copy code --> parse --> AST gen --> bytecode generation --> bytecode interpretation --> baseline jit

Adding layers and layers of git, isn't the solution.  so we can go back and profile.

in the vm parsing is expensive.  parser is lazy and won't parse the fn until it's called.  but what if we could parse it ahead of time.  pre-parse cache.  Now more time in execution than generation and bytecode.

Process: check if there's bytecode for fn, if no then generate AST + bytecode, cache bytecode, and execute.  If there is bytecode, we just execute it.  What if we always had bytecode?  Tried that, called bytecode cache.  Now there's no parsing, it's just execution and small amount of time fetching the bytecode.  Right now this is all android only, experimental (not available yet).

What if you already have a native app and add a bunch of RN features?  Random access bundles.  Imagine yur compiled bundle.  Add hash table to map fn requires to where those modules start and end.  then when you require a model we check if you have done it before, and if you did we return the cached version (bytecode?).  Solves the problem of linear slowdown by the number of RN features you have.

`react-native unbundle --entry-file index.ios.js`

