Building native mobile apps with GraphQL by [Martijn Walraven](https://twitter.com/martijnwalraven)

Apollo client as alternative to Relay

Originally GraphQL was for mobile ios app, but outside of facebook there's still no easy way to use it in native mobile environments.

the main issue with a mobile client is high network latency (sometimes up to several seconds).  you want to avoid repeated roundtrips for the data for a single view.

generate query-specific types

