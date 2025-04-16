# Technical Writing Assignment

For guidance on setting up and submitting this assignment, refer to the Marcy lab School Docs How-To guide for [Working with Short Response and Coding Assignments](https://marcylabschool.gitbook.io/marcy-lab-school-docs/fullstack-curriculum/how-tos/working-with-assignments#how-to-work-on-assignments).

## Prompt 1

In your own words, explain why React is a popular choice for building user interfaces. Make sure to mention at least one benefit, such as how it simplifies development, supports reusable components, or helps optimize performance. Feel free to include any specific features you find particularly helpful.

### Response 1

## Prompt 2

Explain how the useState hook is used in React to manage state within functional components. In your response, include an example of how useState might be used in a simple application and why managing state is important in building interactive user interfaces.

### Response 2

## Prompt 3

Describe the different ways the useEffect hook can be triggered in a React component. Include an explanation of how the dependency array influences its behavior. If possible, provide a code example for each scenario to illustrate your explanation.

### Response 3

The `useEffect` hook can be triggered once at the loading of the app if its dependency array is empty. If the dependency array contains the name of a variable or function, the code written within the hook will commit whenever one of these dependencies is triggered.

For example, the following code logs the message about the starting count once, but whenever count is changed, it logsthe new count to the console

```js
  import React, { useState, useEffect } from 'react';

  const [count, setCount] = useState(0);

  useEffect(() => console.log('Starting Count: 0'), []);

  useEffect(() => console.log(`New Count: ${count}`), [count]);
```

## Prompt 4

The component below makes a mistake when using useEffect. When running this code, we will get an error from React! Please fix this code.

```js
const DogDisplay = () => {
  const [imgSrc, setImgSrc] = useState('https://images.dog.ceo/breeds/hound-english/n02089973_612.jpg');

  useEffect(() => {
    
    const fetchImage = async () => {
      try {
        const response = await fetch('https://dog.ceo/api/breeds/image/random');
        if (!response.ok) throw new Error(`Error: ${response.status}`)
        const data = await response.json();
        setImgSrc(data.message);
      } catch (error) {
        console.error(error);
      }
    }

    fetchImage();
  }, []);

  return <img src={imgSrc} />
}
```

After fixing the code provide and explanation to what you fixed and why it needed to be fixed.

### Response 4

I put the contents of `useEffect` into an asynchronous function and invoked it. Since `useEffect` cannot be asynchronous, another nested asynchronous function was required for the use of `await`.
