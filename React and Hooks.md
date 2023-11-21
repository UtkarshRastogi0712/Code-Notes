#JS/TS 
### Init with vite:
```Shell
npm create vite@latest
```

>Boilerplate shortcut for react component:  rfce (React Function Component Export)

### Index.html and Main.jsx  boilerplate:
#### Index.html:
```Javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Clipnotes</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

#### Main.jsx:
```Javascript
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

### Component boilerplate:
>Component names should always start with uppercase as per react nomenclature.
```Javascript
import 'component.css'
import React from 'react'

function Component(){
	return(
		<div></div>
	)
};

export default Component;
```
### Hooks:
React had built in webhooks support for handling events and states in React applications.
#### useState:
useState provides a way for React to maintain state or value of variables needed throughout the application. It has a simple declaration where in we destructure the variable holding the state and the updater function while initialising the state. It can then be updated in various ways just by calling the updater function with the new value. Provides consistent state throughout the app. Everytime the state is changes, it triggers a re-render;
```Javascript
import {useState} from 'react';

function Component(){
	//Simple state variable with a toggle helper function
	const [state,setState] = useState(false); //initialisation
	const Toggle = () => {
		setState(!state);
	};
	return(
		<ChildComponent toggle={Toggle} />
	);
}
```

#### useEffect:
useEffect is a hook that is used to update values or states or fetch data as and when the state of any of its dependencies changies. It is always executed once at the initial execution of the app and then tracks a the dependencies specifies for change.
```Javascript
import {useEffect} from 'react';

function Component(props) {
	useEffect(() => {
		props.toggle();
	},[props.state]);
}
```

>Note: useState triggers a re-render everytime the state is changed and useEffect is triggered on all re-renders. So if a useEffect hook is tracking changes of a state variable or making changes to a state variable, it effectively creates an infinite loop. A better option to use is useRef.

#### useRef:
useRef is a react hook that is used to reference values or functions or data across the different states of a react App. It is similar to useState in concept but has a few key differences. It updates synchronously, unlike useState and it does not trigger a re-render if it is updated. It has a parameter, current which holds the current value that it is referencing.
```Javascript
import {useRef} from 'react';

function Component(){
	const count = useRef(0);
	function trigger(){
		count.current = count.current + 1;
	}
}
```

#### useMemo:
useMemo is used to memoize (cache) data, functions and other blocks of code and wrap them to change or update only with dependencies to prevent unnecessary state reload of slow functions or functions with large overhead.
```Javascript
import {useState, useMemo} from 'React';

function Component(){
	const [state, setState] = useState(0);
	const doubleState = useMemo(() => {
		return slowFunction(state);
	}, [state]);

	const slowFunction = (value) => {
		//slow memory overhead;
		return value*2;
	}
}
```
### Other libraries:
[[FaceIO]] for face detection as authentication.
[[LongPress]] for longpress events.