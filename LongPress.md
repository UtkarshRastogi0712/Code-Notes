#JS/TS 

Custom react hook to detect longpress events without conflicts from onClick.
### Implementation in longpress.js:
```Javascript
import { useState, useRef } from 'react';

export default function useLongPress() {
  const [action, setAction] = useState();

  const timerRef = useRef();
  const isLongPress = useRef();

  function startPressTimer() {
    isLongPress.current = false;
    timerRef.current = setTimeout(() => {
      isLongPress.current = true;
      setAction('longpress');
    }, 500)
  }

  function handleOnClick(e) {
    console.log('handleOnClick');
    if ( isLongPress.current ) {
      console.log('Is long press - not continuing.');
      return;
    }
    setAction('click')
  }

  function handleOnMouseDown() {
    console.log('handleOnMouseDown');
    startPressTimer();
  }

  function handleOnMouseUp() {
    console.log('handleOnMouseUp');
    clearTimeout(timerRef.current);
  }

  function handleOnTouchStart() {
    console.log('handleOnTouchStart');
    startPressTimer();
  }

  function handleOnTouchEnd() {
    if ( action === 'longpress' ) return;
    console.log('handleOnTouchEnd');
    clearTimeout(timerRef.current);
  }

	return { action, 
			handlers: 
				{ onClick: handleOnClick, 
				onMouseDown: handleOnMouseDown, 
				onMouseUp: handleOnMouseUp, 
				onTouchStart: handleOnTouchStart, 
				onTouchEnd: handleOnTouchEnd } }
}
```

### Use:
```Javascript
import React from 'react'
import useLongPress from 'longpress.js'

const {action, handler} = useLongPress();

function Component(){
	return(
		<Button {...handlers}> Click or Press Me </Button>
	)
};

export default Component;
```