Native Navigation for Every Platform by [Eric Vicenti](https://twitter.com/ericvicenti)

Sharing code not just between platforms, but between apps

Example: two areas of the application that each have their own stack of cards (e.g., different tabs in an ios app).  The problem is we used to use stateful navigators where each tab would maintain its own state.  This isn't ideal because as actions come into the app we have to handle them imparatively. the real problem comes when linking from one area of the application to another because all of a sudden one area of the app needs to know about the rest.

Different approach: declarative navigation views.  use reducer to define our state.  keep state outside of the application but model the same state as the application.  two reducers combined to one reducer that outputs the state.

Good example of open sourced react native app: F8 conference app

Impressive demos of composing cross-platform React native apps.  Uses react-native-web for the web version.  Example code will be open sourced.

NavigationExperimental is a library released earlier this year to improve navigation and keep it stateless.  Now in a better state to innovate on gesture/animations without touching the container.

We want to live into a world where we can `npm install` a chat app and drop it into our application.

We're entering a golden age of shared code in React: sharing code between platforms (native and web).