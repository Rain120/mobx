---
sidebar_label: Collection utilities 🚀
hide_title: true
---

<script async type="text/javascript" src="//cdn.carbonads.com/carbon.js?serve=CEBD4KQ7&placement=mobxjsorg" id="_carbonads_js"></script>

## Object API [🚀]

The Object API is a utility API that enables manipulating observable maps, objects and arrays with the same generic API.

These APIs are fully reactive, which means that even [without `Proxy` support](configure.md#limitations-without-proxy-support) new property declarations can be detected by mobx if `set` is used to add them, and `values` or `keys` to iterate them.

Another benefit of `values`, `keys` and `entries` is that they return array rather than iterators, which makes it possible to, for example, immediately call `.map(fn)` on the result.

That all being said, the typical project has little reason to use these APIs.

Access:

-   `values(thing)` returns all values in the collection as array
-   `keys(thing)` returns all keys in the collection as array
-   `entries(thing)` returns a [key, value] pair for all entries in the collection as array

Mutation:

-   `set(thing, key, value)` or `set(thing, { key: value })` Updates the given collection with the provided key / value pair(s).
-   `remove(thing, key)` removes the specified child from the collection. For arrays splicing is used.
-   `has(thing, key)` returns true if the collection has the specified _observable_ property.
-   `get(thing, key)` returns the child under the specified key.

If you use the access API in an environment in an environment
without `Proxy` support you should also use the mutation APIs
so that they can detect changes.

```javascript
import { get, set, observable, values } from "mobx"

const twitterUrls = observable.object({
    John: "twitter.com/johnny"
})

autorun(() => {
    console.log(get(twitterUrls, "Sara")) // get can track not yet existing properties
})

autorun(() => {
    console.log("All urls: " + values(twitterUrls).join(", "))
})

set(twitterUrls, { Sara: "twitter.com/horsejs" })
```
