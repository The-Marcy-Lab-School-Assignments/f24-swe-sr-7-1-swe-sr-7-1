# Technical Writing Assignment

For guidance on setting up and submitting this assignment, refer to the Marcy lab School Docs How-To guide for [Working with Short Response and Coding Assignments](https://marcylabschool.gitbook.io/marcy-lab-school-docs/fullstack-curriculum/how-tos/working-with-assignments#how-to-work-on-assignments).

## Prompt 1

In your own words, explain why React is a popular choice for building user interfaces. Make sure to mention at least one benefit, such as how it simplifies development, supports reusable components, or helps optimize performance. Feel free to include any specific features you find particularly helpful.

### Response 1

```
In my own opinion, I believe that React is a better choice when it comes to building a user interface. You are able to build these puzzle pieces called components that allow you to put that together to create user interfaces. This also allows for maximum organization, so if something breaks, you'll know exactly where you need to look to fix the problem instead of having to look through a bunch of html divs and tags. Another handy feature is having the ability to simulate multiple pages but really only having one page. By using react router, you are able to change the whole rendering of a page by adding routes to the pages. This gives your site seamless transitions between pages.
```

## Prompt 2

Explain how the useState hook is used in React to manage state within functional components. In your response, include an example of how useState might be used in a simple application and why managing state is important in building interactive user interfaces.

### Response 2

## Prompt 3

Describe the different ways the useEffect hook can be triggered in a React component. Include an explanation of how the dependency array influences its behavior. If possible, provide a code example for each scenario to illustrate your explanation.

### Response 3

## Prompt 4

The component below makes a mistake when using useEffect. When running this code, we will get an error from React! Please fix this code.

```js
const DogDisplay = () => {
  const [imgSrc, setImgSrc] = useState(
    'https://images.dog.ceo/breeds/hound-english/n02089973_612.jpg'
  );

  useEffect(async () => {
    try {
      const response = await fetch('https://dog.ceo/api/breeds/image/random');
      if (!response.ok) throw new Error(`Error: ${response.status}`);
      const data = await response.json();
      setImgSrc(data.message);
    } catch (error) {
      console.error(error);
    }
  }, []);

  return <img src={imgSrc} />;
};
```

After fixing the code provide and explanation to what you fixed and why it needed to be fixed.

### Response 4

the problem with the code above is that programmer made the useEffect callback function async. This means that useEffect would be waiting for a promise to be returned within the callback which in practice, is not the correct way to handle fetches with useEffect. This is a easy fix so don't you fret. All we have to do is remove the async like so...

```js
import { useState, useEffect } from 'react';

const DogDisplay = () => {
  const [imgSrc, setImgSrc] = useState(
    'https://images.dog.ceo/breeds/hound-english/n02089973_612.jpg'
  );

  useEffect(() => {
    const fetchDogImage = async () => {
      try {
        const response = await fetch('https://dog.ceo/api/breeds/image/random');
        if (!response.ok) throw new Error(`Error: ${response.status}`);
        const data = await response.json();
        setImgSrc(data.message);
      } catch (error) {
        console.error(error);
      }
    };

    fetchDogImage();
  }, []);

  return <img src={imgSrc} alt="A random dog" />;
};

export default DogDisplay;
```
