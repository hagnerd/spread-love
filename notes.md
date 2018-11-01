# {...❤️} 🚫🙌
I was tempted to make the title extremely long with many inner sub-titles..

## Spread Love, Not Hype 
### Learning to Let Go, and Love the Future of React

'New' causes strong reactions in people. Some of us get overly hyped and overemphasize the importance of a feature, and while some of us get scared and never give it a chance. Learn the new and upcoming features in React by letting go of production and letting yourself enjoy programming again. 

- - - -
React is uniquely positioned because of its origins at Facebook and the fact that at any time they have 10s of thousands if not 100s of thousands of React components live in production. 

Their promise is to offer backwards compatibility when possible, and long deprecation cycles when it is not possible. 

When a new feature, or pattern comes out, you do not need to re-write every component you have in production. You should feel safe NOT doing so. Facebook certainly doesn't rewrite every component. 

When a feature becomes incompatible Facebook uses code mods to make the upgrade smooth. If they had to manually update every component that used some obscure feature, they would never make a breaking change to React. You should do the same.

Your application is not at risk because React is evolving. Instead the React team is carving an even easier path for you to make even more robust applications in React in the future. This should excite you. 

Learn to let go of the insecurity of code becoming legacy. Don't fix what isn't broken. 

Learn to let go of needing to know everything deeply. Things are moving fast, and you will never be an expert in everything. 

Learn to let go of being productive all of the time. People were productive in jQuery, but this isn't jQuery MPLS. Don't keep your head in the sand. Come up for air. See what's new. Explore. Play. Enjoy.

- - - -
- Thank Nathan for organizing, and React MPLS for the opportunity to speak
- Point people to the slides (hopefully matthagner.com/talks/spread-love)
- "If you want to follow along go to [URL], there will be code examples with links to codesandbox. Feel free to edit them, and play around with them, they will not affect the presentation."
- WHO AM I?
	- three things I'm not
		- A CS Grad or Student
		- A Bootcamp Grad or Student
		- A developer for pay (yet)
	- Three things I am?
- General overview of the talk 
	- With the RFC for Hooks in React I noticed a huge divide in developers, those who were excited, and those who were not. Many in both camps had yet to get a chance to play with the feature. It made me realize how reactionary the development community can be, and the prejudices that are formed without giving things a chance, or hyping them up when we haven't even experienced their down sides.
	- I want us to explore some of these new and upcoming features, from Suspense, memo, and lazy loading which you can use right now if you're on 16.6 >=, to Hooks, and the general concepts surrounding Concurrent React (which is a little more to wrap your head around and currently unstable).
	-  Any questions you have during the talk, just shout out   
	- I've tried my best to avoid stuff like arrow functions and any syntax that is potentially confusing for beginners wherever I can, but there are some places that it is just way more convenient and readable. If you see an example that looks confusing or scary, ask for some clarification and I will gladly do my best to explain, or if you feel more comfortable come up afterwards and I would love to go help you through it. 
- Word of warning
	- Features like Hooks, and Concurrent are NOT set in stone, and there are likely to be some API changes. We are getting our feet with them so they aren't as scary, and so we can all understand the general ideas behind them. 
	- Be open to change.
	- You will learn something tonight
- Deep breath
- Some jargon/clean up stuff
	- Functional Stateless Components are now called Function Components. 
		- Function components were never truly functional by default, and now with hooks they can in fact be stateful so they are neither inherently stateless or "dumb". 
	- Async React is now called Concurrent React
		- The distinction is that while components and resources will load asynchronously, async is much more broad, and what is actually happening is the ability to concurrently load, and pause rendering based on user interaction and app specific needs.  
- 16.6 - Suspense, memo, and lazy 
	- Learn me some of these. 
	- memo is the function component equivalent of React.PureComponent
		- If you've never used PureComponent what it does is shallowly compares all props and states (which means it compares each individual prop, key in state and compares if it is equal) and if any are, then it tells the component to render. 
		- There are some gotchas with deeply nested objects, and functions. Two different objects, even if they have all of the same key value pairs, are never equivalent because JavaScript compares by pointer. If this is over your head, think about it like this. Unless you are comparing (grab something nearby) to itself, the object JavaScript will say they are not equal. Even if it's the same exact type of (whatever it is).
		- It basically implements shouldComponentUpdate() for you and checks everything to see if any have updated. 
		- With memo you do it like so `const Component = React.memo(function component, optional areEqual function)`
		-  `const Comp = React.memo((props) => <div />, () => {})`
		- Unlike the shouldComponentUpdate() method on class components, the areEqual function returns true if the props are equal and false if the props are not equal. This is the inverse from shouldComponentUpdate.
		- Avoid overusing memo or PureComponent. Rule of thumb:
			- If there is a perceived delay in responsiveness,
			- and it can be attributed to unnecessary re-rendering of a component
			- Then implement memo on function components, or PureComponent on class components. BUT ONLY those that satisfy those two rules. 
	- Suspense + React.lazy() (in 16.6)
		- in 16.6 >= Suspense is only useful with React.lazy() which lets you lazily load a component, or resource. 
		- Current benefits of lazy loading are:
			- Not loading assets until needed
			- smaller bundle size sent to clients
			- easier code splitting
	- Rules of Hooks
		- They must be called within a function (not a class, not globally)
		- They must be called at the top level of the function
		- They cannot be called conditionally or iteratively (meaning not within a if/else/switch, or a for/while loop at the top level creating calls to useState/Effect/etc).
			- The order that they are called in matters and is what allows React to track their state across re-renders.
	- Controversy around Hooks
		- Many people had a visceral reaction to hooks.
			- too magical
			- too restrictive
		* There is a misconception with class components in React that causes some of this perceived magic. State actually ISN'T managed within the class component. React does it for you under the hood. State is handled the exact same way for function components with hooks.  When you call this.setState it actually calls enqueueSetState, which is a React internal that creates a pointer in memory for the state of the component, and then reflects that into the state object so you can access it "locally". 
		* You can't conditionally set "state" in class component either. 
	* The Beauty of hooks
		* No more nested-hell-trees (render props and HOCs create an unnecessary nesting layer ever time they're used)
		* Easier to implement
		* Custom Hooks for sharing stateful log + context for sharing state = beauty
	* Warnings!!!!!
		* Implement yourself first! Do not let someone else's abstraction convince you that it is too complicated to do yourself.
		* Do not let someone else's abstraction dictate your code! Hooks are meant to implemented with your specifics in mind.

- - - -
>React 17 = Synchronous Mode (renders are blocking)
React 17 > = Opt-in Concurrent Mode

Show usual loading flow => componentDidMount() loading = true, => data comes in loading = false data = whatever. 

in Synchronous Mode Suspense renders the fallback immediately. If your code loads fast you get the same flash of loading and then the component showing that would if you did the usual loading flow. 

If you opt in to Concurrent mode whether thats in React 17, or while you're playing around with react@next & react-dom@next, then you can set a prop on Suspense called maxDuration which takes the amount of time to wait for the data/component to load before rendering the fallback, in milliseconds. 

You can choose to opt in a portion of the tree by wrapping it in a <ConcurrentMode></ConcurrentMode> component, OR if you want to opt in the whole tree, and the initial render of the application you can use ReactDOM.createRoot instead of ReactDOM.render. 

<StrictMode> 
If you want to prepare for Concurrent mode (whether you're writing a library, or just looking at the upgrade path) you can wrap your application in the StrictMode component, and when you're running in development React will provide warnings about anything that will be a breaking change. This can be old lifecycle methods, the old context api, etc. In production your app will work just fine, but this is a good way to figure out what changes need to be made for your application to be compatible with the future release of React 17
- - - -
things....
- react-cache (reference implementation for libraries/frameworks, you will most likely use a different package depending on your needs and tools. i.e. if you're using Apollo on the front end, they are already working on a concurrent compatible caching system however it might be useful for small one-offs like image caching or caching small requests that you don't need the full framework for).
- scheduler (react will take care of this for you, but if you need more control, or you are writing a library that needs to control this, then you will need to learn it. The API is unstable right now so don't bother learning it concretely, instead learn it conceptually). 'normal priority', 'user blocking priority'.
- Suspense (A react component. You wrap anything you want to catch and provide a fallback for in it. Anything that is not ready to be render will look for the nearest Suspense parent. Meaning you can nest Suspense components. Any sibling children inside of a suspense component will not render until all are ready....)
- lazy() (a react function that returns the promise of a component. Allows dynamic import, and lazy loads). 
- memo (a react function that allows the equivalent of PureComponent, but with function components. args are (Component[,areEqual()]). areEqual is inverse of shouldComponentUpdate for some reason 🤔?
- StrictMode (a component that lets you see if your app/or tree are compatible with upcoming 17/concurrent mode. It shows warnings in development, but does not effect production mode).
- ConcurrentMode (a react component that lets you optionally opt into concurrent mode. If using react@next and react-dom@next aka 16.7alpha, it is under unstable_ConcurrentMode you can wrap the whole app, or just portions of it in ConcurrentMode).
- createRoot (a react-dom function that opts into concurrent mode for the whole tree. Replaces render).

- - - -
QUESTIONS TO ASK THROUGHOUT:
- How many people have used an ErrorBoundary? (If low, maybe show how to implement one). They will be important in ConcurrentMode because if something goes wrong, it will throw and error. It's better to have it catch and display an ErrorBoundary component than have the whole app crash and go to shit. 
- - - -
## SECTIONS
### Intro
#### 16.6 - Suspense (sync), memo, and lazy
####  
