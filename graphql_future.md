GraphQL Future by [Lee Byron](https://twitter.com/leeb) and [Laney Kuenzel](https://twitter.com/laneykuenzel)

GraphQL Recap

Not just a library, so it's strange to open source.  At Facebook our servers are written in Hack, so releasing Hack code to Github wouldn't be as useful.  So they wrote a specification.  In addition to that they released a reference implementation of that spec in JavaScript.

GraphiQL is an editor and query explorer that runs in your browser.  It's important to how they use and teach GraphQL at Facebook.  They released GraphiQL last fall as open source.  A lot of GraphQL server implementations just enable it by default.

GraphQL is now available in over a dozen server side languages: Ruby, PHP, Python, C++, Java, Go, Scala, Haskall, Lua, Elixer

GraphQL Clients: Relay, Lokka, Adrenaline (with Redux), Apollo (Redux + other view libraries and native apps)

We're seeing companies and services launching that help you get a GraphQL server up and running (Reindex, Graphcool).  New startups forming around GraphQL.

There's a burgeoning GraphQL ecosystem.

No matter what your tech stack looks like on the back or frontend there are libraries to help you get started with GraphQL quickly.

Meanwhile, at FB they've been busy updating their GraphQL clients to use the open source clients.  GraphQL has been used at FB for over four years now.  Now they're updating to the latest version, and thinking about the future (experimental!).

FB only open sources what they use in production, and what is generally useful.  But they experiment in the open, and include them in GraphQL once they've proven themselves.

What problems should GraphQL solve?

* Clients express what they need (curb over and under fetching and remove the need to version your APIs).
* Minimize network reqeusts, especially when your app needs multiple resources.
* Colocate data needs to reviews.
* Strong types: cool tools, but also predictable and well typed data.

But today GraphQL only handles one way to get data: `GraphQL Request => Promise<JSON Response>`

New Problems:

1. Time to important data: currently you need to wait for all data to be prepared before you can use it
    * Just send two network requests?  Sure, but it's not as efficient as we'd like.
    * Can we do it in one request?
        * GraphQL Batch: multiple independant queries in one request, and declare deps between them. This is in production use at Facebook right now.  But still issues with this.
        * `@defer` is an earlier stage experiment. Lets you mark part of your query that you want to wait on.  And you get the multiple JSON bodies over time, with the later one as a patch object. (not in production at FB)
        * `@stream` delays part of your query but schedules each story in a list down as a patch. (not in production at FB)
2. Real-time data updates: reactive servers, and GraphQL doesn't have the ability to do this yet
    * Current solution? Repeated polling with the same query. Simplest way to get data to the app.
    * Existing mechanisms: Websockets, 0MQ, Notifications.  but all have their problematic cases.  it's really common for these payloads to under or over fetch.  and versioning issues.
    * Reactive backends and databases such as RethinkDB and Reactive Extensions.  You have observables, you subscribe to those, they flow data through your machines, recompute data on the fly, and anyone subscribing gets those pushes.  But this is an architectural invesment.
    * `@live`: Beginnings of a GraphQL experiment with supporting live data from reactive backends (not yet in production)
        * Facebook doesn't have a reacive infrastructure currently
    * GraphQL Subscriptions
        * Intricate data depenencies so it's not feasible to determine when a field has changed based on actions
        * Instead, they went with event based subscriptions
            * Clients subscribe to an action with a GraphQL query for what data they want when an event happens.
            * When the event happens they receive payloads answering that query they subscribed with
            * Every type of subscription has publish trigger that needs to be called when event happens. This lives where comments get created.
            * Many different subscribers to the same topic but with different queries
        * Live likes and comments, reactions during video, whether your typing (in production at FB)
        * Challlenges: throttling


