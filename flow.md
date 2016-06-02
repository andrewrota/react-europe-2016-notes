A Deepdive into Flow by [Jeff Morrison](https://twitter.com/lbljeffmo)

Flow is a static type checker for JavaScript.

It's become clear that type checkers are a black box to most people, so this talk will dive into the details of how it works.

Stages of flow:

1. Parse: into an AST
2. Infer: traverse (depth first) the AST and extract information
    * First area in memory it deals with is scope.  Table that goes from var name to var type.
    * Type heap is where we store all the types in Flow. Each type is represented by a tiny data structure.
    * Example `var a = 'abcd'; a.lenght;`
        * Give a an open type, a placeholder for a type that we'll figure out later.
            * All types have a name, and all those names end in a capital T, and they all carry around data.  So `OpenT {id:0}`.
        * Create type `StrT` for string and store data with it, so `StrT {value:"abcd"}`
        * String flows into a, via a flow constraint which is a link between two types.  This is where we start to see how Flow differs from other type checkers.
            * Typically type checkers are eager to figure out the type of a variable asap.  In flow they don't take that approach because it turns out in dynamic languages like JS this is bad: problems with null.
        * Check property `lenght` on `a`.  Create special type called `GetPropT`.  This is different from the other data types: it's a use type which describes actions on other types.  It's `GetPropT { prop: 'lenght', result: OpenT{id:1}}`.
            * Add flow constraint between `OpenT{id:0}` and `GetPropT`.  Now we have a flow graph that's more valuable than an AST.  All we eed going forward is the flow graph.
3. Evaluate: run through that graph and see if we can find any problems with it.
    * start at the bottom.  If we encounter a flow constraint we'll look up what to do for that constraint and do it.  What do we do when a `StrT` flows into `OpenT`? The rule is whatever flows into `OpenT` gets flowed directly to what `OpenT` was flowing to.
    * When `StrT` flows into `GetPropT` we create two new types, `InstanceT {name: 'String', parentClass: prototype, members: PropMap` (instance of object with some data in it) and `LookupT` which is similiar to `PropT` except it looks up the prototype chain.
    * Flow the result of the `LookupT` to the result of `GetPropT`.  `OpenT{id2}` to `OpenT{id2}`
    * Rule says if you don't find prop in the members class you flow that into LookupT. Create new InstanceT, repeat.  Exactly the same thing a JS VM is.  If we don't see a prop, we go up a level until we find it an return.  We're just doing that at a type level.  In a VM if you get to the top of a prototype change you return undefined and that's not helpful.  So in flow we model that at the top of the prototype chain is `MixedT` which is a black hole type.  Anything flows into it, nothing can be pulled out of it.  So the rule for `MixedT` flowing into `GetPropT` is a type error.
    * `a.lenght property 'length' not found in 'a'`  Yay!

That's source code to type error in a single module.  In a real application you have multiple modules, so we're going to just draw a line around these types to indicate that they're in one module and do that process in parallel for different modules.  But also in real life modules have dependencies on eachother.  So what happens when two modules depend on eachother?  In flow, we treat it as a flow of one module to another module.  Flow constraints that cross module boundaries (an import or an export).

Lots of interesting things you can do with flow graphs rather than just type checking.

* Taint analysis: you can trace through your application all the places data in your application is going to go.
* Super precise tree-shaking: can see which properties on objects aren't being used and delete them.

@flowtype, github.com/facebook/flow

**Not just a typechecker: a platform for code intelligence**
