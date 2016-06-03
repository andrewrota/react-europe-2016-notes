Building li.st for Android with Exponent and React Native by [Brent Vatne](https://twitter.com/notbrent)

Insight into perspective of someone working with React Native every day for the last year.

* Lists: incremental and lazy rendering
    * incremental rendering: rather than rendering all the views in your list upfront and blocking the thread unnecessarily, you chunk it into smaller pieces and occasionally yield
    * windowed list view: rather than keeping earlier rows in memory, it just renders rows in a certain window and removes the rows as you scroll past that and replaces with a spacer view.  Trade offs: it's more CPU intensive
    * Native list views (UITableView) reuse the rows and move them into a recycling pool when they're not used, but that's not available in react native yet

* Offload your animations
    * It's pretty easy to get into a situation where animations block the JS thread.  Every frame it has to call back and do JS to update the value.
    * One solution is InteractionManager which allows you to pass in a callback that's executed after all animations/gestures are completed. This can still lead to slow feeling apps in some cases because we sequence fn one after another careful not to drop frames. so you may need to decide whether to offload the animations.

* Navigation
    * In ReactNative you need to use a navigation API of some sort.  It shipped with Navigator, and it was a good first attempt.  but still tricky, for example with offloading animations since Navigator was created before the animation API existed.  switched to NavigationExperimental because it's powered by Animated.  [ex-navigation](https://github.com/exponentjs/ex-navigation).

* User input: text
    * user input has difficult pieces.  keyboard behaves differently on ios and android, and you have to watch for keyboard events all over the place (i.e., change interface layout based on keyboard appearing by adding a spacer to the bottom).
    * control cursor selection position if you change the length of the text in response to a change event, otherwise the cursor just won't go where you want it to go.
    * Growing text input doesn't come with React Native, and a lot of times when you have multiline text it starts with one line and grows when you add text.  They wrote a component for this

* User input: touch & gestures
    * You can get around most limitations today in react native without too much work
    * Gesture system doesn't work well when a comple components are interested in a single touch event

* Living in Production
    * Source Maps don't always work perfectly.

* Contribute upstream
    * React Native is still new enough that if you're using it you'll discover bugs no one has fixed