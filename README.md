# Technical Writing Assignment

For guidance on setting up and submitting this assignment, refer to the Marcy lab School Docs How-To guide for [Working with Short Response and Coding Assignments](https://marcylabschool.gitbook.io/marcy-lab-school-docs/fullstack-curriculum/how-tos/working-with-assignments#how-to-work-on-assignments).

## Prompt 1

In your own words, explain why React is a popular choice for building user interfaces. Make sure to mention at least one benefit, such as how it simplifies development, supports reusable components, or helps optimize performance. Feel free to include any specific features you find particularly helpful.

### Response 1

React is a popular choice for building projects because it streamlines the DOM manipulation process and makes the connecting javascript functionality with HTML elements more efficient. One of the biggest benefits is that React is written with HTML-like syntax, so all the tags and attributes that one might be familiar with in HTML translate really well into React.

## Prompt 2

Explain how the useState hook is used in React to manage state within functional components. In your response, include an example of how useState might be used in a simple application and why managing state is important in building interactive user interfaces.

### Response 2

In React, we can create a Counter component that initializes with a value of 0 when the page loads. Whenever the user clicks on the counter, its value should increase and update dynamically on the screen. To achieve this, we use the useState hook, which allows React to track and manage state changes efficiently. When the counter’s state is updated using the setter function from useState, React detects the change and automatically re-renders the component, ensuring that the displayed count always reflects the most recent value.

Example Code:

```javascript
import React, { useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0); // Initialize state with 0

  return (
    <div>
      <h1>Counter: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
};
```

## Prompt 3

Describe the different ways the useEffect hook can be triggered in a React component. Include an explanation of how the dependency array influences its behavior. If possible, provide a code example for each scenario to illustrate your explanation.

### Response 3

useEffect has 2 parameters, the first being it's function i.e. what will happen when useEffect triggered,. The second parameter is what determines what things trigger the page to re-render, it's referred to as its dependency, and this parameter has a couple of different configurations.

1. _No dependency_: when a dependency isn't provided, the useEffect's function will run _every time_ the page is _rendered_ and _re-rendered_. looks like this:
   ```jsx
   useEffect(() => {}); //nothing after the function
   ```
2. _Empty array_: when an empty array is passed in, the useEffect's function will run _once_ after the _initial_ render of the page. looks like this:
   ```jsx
   useEffect(() => {}, []); //empty array after the function, separated by a comma
   ```
3. _Array with values_: when an array with _dynamic values_ is passed in, the useEffect's function will run _every time_ those values _change_. looks like this:
   ```jsx
   useEffect(() => {}, [a, b]); // re-renders when a or b change
   ```

## Prompt 4

The component below makes a mistake when using useEffect. When running this code, we will get an error from React! Please fix this code.

```js
const DogDisplay = () => {
  const [imgSrc, setImgSrc] = useState(
    "https://images.dog.ceo/breeds/hound-english/n02089973_612.jpg"
  );

  useEffect(() => {
    const fetchHandler = async () => {
      try {
        const response = await fetch("https://dog.ceo/api/breeds/image/random");
        if (!response.ok) throw new Error(`Error: ${response.status}`);
        const data = await response.json();
        setImgSrc(data.message);
      } catch (error) {
        console.error(error);
      }
    };
    fetchHandler();
  }, []);

  return <img src={imgSrc} />;
};
```

After fixing the code provide and explanation to what you fixed and why it needed to be fixed.

### Response 4

The useEffect React hook was orinally declared as an async function which is not correct because as we know async functions return promises and React's useEffect expects the function to return nothing (undefined) or to return a clean up function that runs when the component unmounts.
