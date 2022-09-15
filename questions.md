## What is the difference between Component and PureComponent? give an example where it might break my app
PureComponent and Component are almost the same. The difference is in the ShouldComponentUpdate method behavior, in PureComponents this method makes a shallow comparison for props and states, checking if their references are changed instead verify all structure trees. This shallow comparison can bring improvements in performance

## Context + ShouldComponentUpdate might be dangerous. Can think of why is that?
If ShouldComponentUpdate returns false, the component will not take the updated Context and the component will keep using out-of-date data.

## Describe 3 ways to pass information from a component to its PARENT

**1. Passing a callback method as a property**

When the child component calls this callback method, this value is passed to a function that is owned by the parent component that can manipulate the received data

**2. Using Context**

When a component is wrapped by a Provider, it has access to any information contained in this scope. If any data of this scope were modified by a child component, the parent component will have access to these updated data.

**3. Passing a state setter as a property**

When the child component calls this state setter, it will call a function that will directly update the parent component's state.

## Give 2 ways to prevent components from re-rendering

React.memo does a shallow comparison between component's previous and new props, and if they're the same the component will be not re-rendered.

Use useRef instead useState for situations where it's necessary to keep some data but this information doesn't need to be shown on the screen.

## What is a fragment and why do we need it? Give an example where it might break my app

With the Fragment, it's possible to return multiple elements on a Component without using a DOM node.

Using Fragment to wrap the components, will reduce the load on the DOM, resulting in faster rendering times and decreased memory usage.

Since Fragment does not create an extra DOM node, it avoids issues when using CSS with components that must follow a specific hierarchy.

In the case of being returned instead of returning null, the Fragment can decrease the performance, since it will be something unnecessary to be processed by React.

## Give 3 examples of the HOC pattern
### #1
    const  logOnRender = WrappedComponent  =>  props  => {
	    useEffect(() => {
		    logMessage('Component was rendered')
	    }, [])
	    
	    return <WrappedComponent  {...props}  />
    }

    export  default  logOnRender(SomeComponent)

### #2

    const  withSomeContext = WrappedComponent  =>  props  => {
	    const { value, setValue } = useContext(SomeContext)

		return (
			<WrappedComponent
				{...props}
				value={value}
				setValue={setValue}
			/>
		)
	}

	export  default  withSomeContext(SomeComponent)
### #3
**connect()** from **Redux**

## What's the difference in handling exceptions in promises, callbacks and async...await?
**Promise:** In a case of a rejected promise we use the .catch to get the error

**Async/Await:** We must use try/catch to capture the error and avoid a break by some exception

**Callback:** In general, if some error occurs it will be received as an argument on the callback function

## How many arguments does setState take and why is it async?

setState takes two arguments. The first argument can be the new value or a function that receives the current state and props as parameters and returns some value, this returned value will be the new value of the state. The second argument is optional and is a function to be called once setState is done and the component is re-rendered.

setState is async because the state value will not be changed until React re-renders the component, passing the new value.

## List the steps needed to migrate a Class to Function Component
1. Remove the constructor
1. Use useEffect instead componentDidMount (with an empty array of dependencies) and componentDidUpdate
1. Create the initial state using useState
1. Use return instead the render method
1. Turn in variables the old class methods
1. Remove references to "this" on the component
1. If necessary, split the old state into new small-scoped states and use the right update-state method for each case

## List a few ways styles can be used with components

1. Including styles in the HTML file
1. Using inline css through the style prop
1. Importing a css file inside of a component
1. Using styled-components
1. Including the style tag in the returned elements of the component

## How to render an HTML string coming from the server

Using dangerouslySetInnerHTML after sanitizing the HTML in order to check if it has some scripts or other malicious code