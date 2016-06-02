GraphQL at Facebook by [Dan Schafer](https://twitter.com/dlschafer)

Hello world of GraphQL:

```
{
  me {
     name
  }
}
```

...and you get back json in the same shape.

As you need to fetch different data you just change that shape.  Can also select sets of data in the same request.

When we talk to graphQL we are mostly talking about the API and the server implementation.  this talk focuses on the server implementation.

Three core principles of FB's GraphQL stack:

1. Think graphs, not endpoints.
2. Single source of truth
3. Thin API layer

Authorization.  Should live at business logic layer, not storage or REST layer.  Use a `gen` method in your class where you handle fetching and authorization.  Can a given viewer see a given piece of data?  Static method that takes in a viewier and id, and returns the object or `null`.  This pattern is ubiquitous in the Facebook codebase.  **You want the easiest thing to do to be the thing that is correct.**  In GraphQL there's a third arg for a viewer that's gotten via oAuth or something and that threaded passed through to canonical authorization logic.

Efficiency.  Batch multi requests.  Don't implement batching in graphQL, implement it in the business logic layer.  Does that with a package called DataLoader by FB.  Define a new DataLoader and let that handle the batching.  But you might still be overfetching.  Caching on the server is particularly important here.  But our clients also want caching, and we can't use HTTP caching with GraphQL.  We need a unique key.  We have that on the server (which caching is implemented based on) so we can expose that to the client.  What do we want in IDs?  In a dream scenario it's globally unique and it's a refetch identifier.  Client comprehension of ID is an antipattern here.  IDs should be opaque to clients, other than that they're globally unique and can be used for refectching.  FB is `base64('user:1')`.