---
title: Using React hooks in class components
layout: post
---

Unless you’ve been living under a rock for the last 6 months you’ll know that hooks in React are the new hotness. There’s now a hook covering almost every single browser API plus many more. Adoption in the community has been widespread to say the least.

Hooks aren’t perfect right now, their API doesnt fully replace class methods yet and [developers are still learning how to use them effectively](https://overreacted.io/a-complete-guide-to-useeffect/); it's [a brand new paradigm](https://overreacted.io/react-as-a-ui-runtime/) to learn. In large codebases lots of legacy components still use classes, but you might want to use some awesome behaviour you’ve added in a new hook without having to rewrite code.

What if we could use these hooks we've written in class based components?

One option is to import another library that (probably) doesn’t use hooks and use their existing API. This is bad for several reasons

* More dependencies means more code and therefore higher surface area for bugs
* Multiple dependancies doing the same or similar things
* Additional chores when upgrading
* Higher bundle size

There is however a way you can write new behaviour as hooks and still use them in class components.

## Hooks first

Imagine a straightforward hook that uses the [`window.online`/`window.offline`](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorOnLine/onLine) events to monitor if the user’s device is online. If the user goes offline we might want to re-render and show an error message instead. When the user reconnects to the network we want our app to render the UI again. In reality you’d probably want to [make your app more progressive](https://developers.google.com/web/progressive-web-apps/) but this simple example will do for our purposes:

```jsx
import useNetworkMonitor from 'useNetworkMonitor';

const App = () => {
	const isOnline = useNetworkMonitor();

	return isOnline ? <Index /> : <OfflineError />;
};
```

One of the benefits of hooks is that they reduce cruft in your component tree. Over the last few years as the render props pattern has taken off we’ve started seeing more components being rendered that don’t have any influence on the UI, they’re just passing state and props down to another component. These components are important as they allow inversion of control; your child component can access state from within the parent component without them having to know about each other. However, as they start piling up in your components, you'll find that the component tree becomes polluted and therefore debugging becomes harder.

Although hooks aims to reduce these kinds of components, we can actually leverage them to add support for classes via render props with minimal extra code:

```jsx
const NetworkMonitor = ({ children }) => {
	const isOnline = useNetworkMonitor();

	return children({ isOnline });
};

<NetworkMonitor>
	{ ({ isOnline }) => (
		isOnline ? <Index /> : <OfflineError />
	) }
</NetworkMonitor>
```

What if you're already using the render props pattern to add behaviour like this in an existing code base using a class based component? Good news, you can convert your render props component to a hook, implement the above pattern and slowly over time phase out usage of the class component.

The points discussed in this article are probably not a massive revelation to most readers but they are important. Right now the React API is undergoing a transition as `Suspense` and async rendering comes along; established patterns and best practises are changing rapidly. I’d really love to see hook authors start implementing this bridge component pattern, allowing both modern and older React code to play together nicely as well having as a clear migration route towards a hooks based future.

## Going even further with higher order components

Remember HOCs? You might still be using them. Well we can apply the same pattern here as well:

```jsx
function withNetworkStatus(ComposedComponent) {
	return function NetworkMonitorWrapper(props) {
		const isOnline = useNetworkMonitor();

		return <ComposedComponent { ...props } isOnline={ isOnline } />;
	};
}

// <Index /> component now has an isOnline prop injected
withNetworkStatus(Index);
```

This is probably one step too far. Don’t do this.

## Summary

So just to recap:

* Write your hooks as you have been doing already
* Add a render props / function-as-child bridge component for use in class components
* Add a HOC if you’re a little bit crazy
