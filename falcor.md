Falcor by [Jafar Husain](https://twitter.com/jhusain)

Falcor is a data fetching library built for the needs of modern applications.

Why another one?

Falcor exposes all data stores in the cloud as a single JSON resource.  Clients use falcor to request just the fragment of the request they need.  Once on the device falcor caches it so it doesn't need to request that data again.

David Nolen coined a term for this architecture: demand driven architecture.

Falcor isn't the only game in down when it comes to demand driven architecture: graphQL is another one.

At a high level, GraphQL and Falcor are both tackeling the same problem in similiar ways.

Netflix thinks there's space in the ecosystem for both of these technologies.  Each have different trade offs.

Falcor is simply less prescriptive than GraphQL, and as a result it may be able to adopt and integrate into your stack in a more gradual way.  It's also alot smaller than GraphQL.

You don't need to define a schema and you don't need to learn a query language: difference from graphQL.

one of the challenges with working with json data is that sometimes you can get duplicates.  graphql solves this by having unique identifiers for models.

falcor introduces an extension to json called jsonGraph.  it's a filesystem with symbolic links.  you can convert any json object into jsonGraph, which is basically a convention for modeling your graph in json syntax.  json + references.

what's best for your app (graphQL or falcor)?  broadly speaking both are creating this abstract conceptual model for requesting data on demand.

**GraphQL**

* Schema required
* Retrieve data with query syntax
* Cache data and update components
* Built in schema
* Built in tools (GraphiQL)
* Runtime schema reflection
* Syntax is uniform way of querying any collection
* Challenging to implement, leaky abstraction, need to be more defensive
* Good for apps for which data transformations are dynamic and unpredictable

**Falcor**

* Optional schema (falcor doesn't require a particular type of schema)
* Retrieve data with JS paths
* Cache data
* Iterate fast, then apply schema
* Integrate with existing type system
    * TypeScript
    * JSON Schema
* Falcor takes advanage of the fact that any _pure_ function can be represented as a map
* Good for apps where transformations are modest and known ahead of time


Depending on how big the surface area of your type system it may make sense to have a schema.

Graph QL handles requst evaluation and Relay handles device caching and component updates.  Falcor handles request evaluation and device caching, but lets applications handle their own component updates.

Falcor supports vanilla react data stores, single flux stores, access data in redux middleware.

