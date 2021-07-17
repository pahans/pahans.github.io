---
title: State Management in a React App in 2021
---

A most common pattern is using React for UI rendering and Redux **global** state management together with [Flux pattern](https://facebook.github.io/flux/docs/in-depth-overview/#:~:text=Flux%20is%20the%20application%20architecture,a%20lot%20of%20new%20code.). Before you put your app into Redux rabbit hole consider [whether you actually need Redux](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367). This is a very higher-level view of a frontend component architecture. We should shape architecture to promote code readability, maintainability, debuggability, testability, and better separation of concerns.

I’ll explain each section in detail from the bottom up.

![](/images/migrated/1__Td__BjatOZFGBfRQrTb__LAA.jpeg)

#### Presentational Components

The separation of the presentational and container components was a decision inspired by [Dan Abramov’s blog post](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0).

Presentational components are…

1.  Only responsible for the DOM markup.
2.  They get data via props and communicate back only via callbacks we passed on as props.
3.  They might have a state, but most of the time, the state is lifted up to a container component and passed to the presentational component via props.
4.  Since presentational components are loosely coupled it’s really easy to reuse them.

#### Container Components

This is where most of the business logic happens. Container components “contain” presentational components. Container components are responsible for…

1.  Fetching data from backend APIs and forward them as props for presentational components.
2.  Composing dispatchable actions as callbacks for presentational components.
3.  Passing data from global store to presentational components.
4.  Storing local state/callbacks to trigger actions lifted from presentational components.

Container components are not reusable but we can break them into reusable smaller units like custom hooks which I will discuss later.

#### APIs

Previously I used to [fetch data from APIs via redux](https://redux.js.org/tutorials/essentials/part-5-async-logic) but I would discourage that now because,

1.  Lots of boilerplate code to fetch data from an API. It’s a boring repetitive task.
2.  Pollutes the global state.
3.  Having to make redux state async adds additional complexity to the code base.
4.  API calls are duplicated if we want the same data in several components. So it impacts application performance. Of course, you can dedupe them with prop drilling but again it’s additional complexity.
5.  Duplicated API calls also mean additional renderings. Again it impacts application performance.

And the answer I found for the above problem is …

#### Alternative Approach to Data fetching — Custom Hooks

Custom Hooks allow us to extract component logic into reusable functions. It’s not something specific for data fetching but let’s focus on our use case for now. Instead of building our own hooks from the scratch, I opt to use the [SWR](https://swr.vercel.app/) library which addresses the problems above plus a bit more. There are alternatives like [React Query](https://react-query.tanstack.com/) too.

SWR makes our life easier with…

1.  A builtin cache for request deduplication
2.  Builtin optimistic rendering — first return the muted data from cache (stale), then send the fetch request (revalidate), and finally, come with the up-to-date data.
3.  Automatic retry on error.
4.  Polling on interval.
5.  Data revalidation on focus (If the user switch browser tabs or returned after locked ).

#### Redux Store

Since we use custom hooks for data we only have few use cases to use the redux store. as [I said earlier we might be better off without redux.](https://dev.to/g_abud/why-i-quit-redux-1knl)

That’s it, this is how I think we should build a frontend React app in 2021. If you have any questions/suggestions feel free to leave a comment. In the next post, I will share how to accommodate automated testing into this architecture.