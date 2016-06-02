On the Spectrum of Abstraction by [Cheng Lou](https://twitter.com/_chenglou)

software engineers seek concrete use cases rather than abstractions themselves (computer scientists seek abstractions, not instances)

power is to drill down from the abstractions to the use cases.  utility is on the other end of the tree.  a use case is useful if you don't need to think about the abstractions.  In this context, react is not very useful.

The bad part about software engineering is that if you want to drill up or down the levels of abstractions there's a cost.  we want to cover all the leaf nodes with the least amount of cost.

 principle of least power: if you want to cover all these use cases then you probably want to use the least powerful tool to achieve that because there's less mental overhead.

 library vs. framework is just a specialization of this paradigm.  libraries are choosing abstraction nodes lower in the tree, frameworks are choosing nodes higher in the tree but that's ok because other people will need those use cases (this choice is half engineering and half social)

 micromodules would be abstractions for each of the use cases.  the problem here is there are too many of these so there's soo high quantity.

 "lots of problems arise from a bad understanding of where we should be in the levels of abstraction"

 writing code is easy.  if you get your abstraction wrong, no amount of editor refactoring can correct that.

 more abstract --> lose situational-specific properties.  Properties here are the things we want to maximize as engineers

redux limits your expressivity in a good way by saying no mutability.

"we're often not seeking for more power. we're seeking for more principled ways of using our existing power."

Reduce expressivity in a principled way.  Instead of goto we have for loops.  Instead of for loops we have map/reduce.

what properties arise from having constraints?

Case Studies

**grunt vs gulp:** Declarative DSLs work very well when your domain is well defined.  when you use a declarative build system and does what you want it's very convenient.  but when it doesn't work, you have to twist it to get it to work.  Why is this relevant for a build system?  Requirements in build systems are constantly changing, so do you want a declarative DSL or use functions that are more flexible for future use cases.

**react vs templates:** templates are data (lower level of abstraction) but the situtation of the web has changed, and js is used for more than just interactive forms. but if you're building full interactive apps then maybe you should step up a level of abstraction.  this is a concession.  but we're going with it because we need an extra level of expressivity.  ember limiting expressivity means they get more performance out of it.  theoretically jss/fns loses performance at the benefit of gaining expressivity.

**diffing on view vs. diffing on model/computation:** here react goes with the former because it's data and they get performance gains here.  difffing on the model is data, but you have a whole chain of computation after the model, and because you can't compare the computations you lose those properties and you have to restore them somehow (the solution is computed properties, but this is less convenient according to react)

**Immutability vs. mutability:** you can do strictly more with mutability so why choose something that's powerful.  but that's not the point.  it's not about the potential power, it's about exploiting the properties you gain by doing less.  because you're doing less with immutability you gain a lot of features (e.g., time travel).  all of that from doing less, not more.

**JS (inline) CSS vs Traditional CSS:** one good argument against js css is that giving a layout language the power of js is a problem.  CSS is less powerful/expressive, so if we can do everything with CSS in theory you should.  You have more power with CSS, for example, to be able to statically analyze.  But we don't do that, and prepreocessors show us a declarative DSL isn't enough.  This is at the heart of the argument for JS CSS.

Concrete Experiences:

* Don't cover every use-case.  THe easiest way to optimize is to do less work.  React supports a small API surface area to support optimization potentials. don't constain yourself too much so you don't have any wiggle room.
* Not DRY (i.e., repeating code) is fine.  Cost to abstract things vs. using them.
* Don't be swayed by elegance.  elegance is an overloaded term, sometimes we mean it to be a single unifying principles and as engineers it can be attractive to explain everything with one thing. but you can bet it's very difficult to understand for the user.
* When in doubt, use examples. We use examples because examples on the tree of abstraction are on the very lowest level.

Conclusion

This talk, on the levels of abstraction, is very high in the tree, so it's the most useless talk of the conference.  but now you know the definition is consistent!

Apply don't think in theory only!