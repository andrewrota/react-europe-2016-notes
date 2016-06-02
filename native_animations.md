React Native <3 60FPS by [Krzysztof Magiera](https://twitter.com/kzzzf)

Animations for: transition, focus, fun

Animation types in React Native:

* Native components animations: native components in the platform, use by rendering component, i.e., `<NavigatorIOS/>`, `<MapView/>`, `<TouchableNativeFeedback/>`, `<ViewPager/>`.  JS has nothing to do with these.
    * Pros: max performance, platform-specific behavior by default, very little work
    * Cons: very limited set of components, often impossible to customize
* Layout animations: i.e., `LayoutAnimation.spring()` before you change the state. JS thread --> native thread --> UI thread.
    * Pros: native performance, very easy API
    * Cons: works for layout properties only, non-interruptible
* Animated.js: "focuses on declarative relationships between inputs + outputs".
    * Pros: very flexible, allows for defining gesture interaction, best performance when not animating layout props
    * Cons: difficult to express layout animations - complementary API is needed

Perf Monitor in React Native devtools gives you info on fps, frames dropped.

Animated.js has been designed performance in mind and React Native in mind.  Works to move work JS does for animating onto the native side.  Generate animated graph in JS and move it to the UI thread.  `useNativeDriver: true` whenever you start animations.  Some limitations still (Android only (PR yesterday for iOS), only a subset of Animated.js is implemented, animating layout props probably won't be supported).