# How to make an scroll to the top button component in React

## Description

Have you ever read something on a website and got annoyed because it did not have a scroll to the top button? Well, let's see how to make one ourselves.

## Requirements

- Code Editor
- React.js
- `styled-components`
- `yarn` or `npm`

## Introduction

It is frustrating when you are scrolling through a page and when you want to go back to the top and you don't have the ability to do it quickly, I mean, if the developer feel the pain, the user mind as well close the page altogether 😂. It really hurts the **user experience** and the problem should be addressed.

So lets code a little component to address this problem.

## Lets code

Firstly lets make our base code for the component:

```jsx
import React from "react";

const ScrollButton = () => {
  return <h1>Hello World</h1>;
};

export default ScrollButton;
```

Ok, now we're gonna need the `HTML` button itself and an icon with an excellent little library called `react-icons`:

Add the library:

```javascript
yarn add react-icons
```

Or:

```javascript
npm i react-icons
```

Then add it in the component:

```jsx
import React from "react";
import { BsArrowUp } from "react-icons/bs";

const ScrollButton = () => {
  return (
    <button>
      <BsArrowUp />
    </button>
  );
};

export default ScrollButton;
```

Now we have to build our helper functions. Starting with the function that will make the scroll to the top:

```jsx
import React from "react";
import { BsArrowUp } from "react-icons/bs";

const ScrollButton = () => {
  const scrollOnClick = () => {
    window.scrollTo(0, 0);
  };

  return (
    <button onClick={scrollOnClick}>
      <BsArrowUp />
    </button>
  );
};

export default ScrollButton;
```

The `scrollTo` method scrolls the document to the specified coordinates, so (0, 0) should scroll to the top of the page.

Now we need a helper function so we know where we are positioned on the screen:

```jsx
const handlePosition = () => {
  if (window.scrollY >= 200) {
    // do something
  } else {
    // do something
  }
};
```

The function has to store the information on the state so:

```jsx
const [scrolled, setScrolled] = React.useState(false);

const handlePosition = () => {
  if (window.scrollY >= 200) {
    setScrolled(true);
  } else {
    setScrolled(false);
  }
};
```

The `scrollY` property of the window interface returns the number of pixels that the document is currently scrolled vertically. So by comparing it in the `if` conditional statement by 200 we should find out if the page is scrolled beyond 200 pixels vertically.

Now we are gonna need a `useEffect` hook to listen to the scroll event on page load:

```jsx
const handlePosition = () => {
  if (window.scrollY >= 200) {
    setScrolled(true);
  } else {
    setScrolled(false);
  }
};

React.useEffect(() => {
  window.addEventListener("scroll", handlePosition);

  return function cleanup() {
    window.removeEventListener("scroll", handlePosition);
  };
}, []);
```

The `addEventListener` method attaches an event handler `handlePosition` to the specified element `scroll`. Then to clean up the `useEffect` hook, you need to `removeEventListener`.
The partial code should be this:

```jsx
import React from "react";
import { BsArrowUp } from "react-icons/bs";

const ScrollButton = () => {
  const [scrolled, setScrolled] = React.useState(false);

  const scrollOnClick = () => {
    window.scrollTo(0, 0);
  };

  const handlePosition = () => {
    if (window.scrollY >= 200) {
      setScrolled(true);
    } else {
      setScrolled(false);
    }
  };

  React.useEffect(() => {
    window.addEventListener("scroll", handlePosition);

    return function cleanup() {
      window.removeEventListener("scroll", handlePosition);
    };
  }, []);

  return (
    <button onClick={scrollOnClick}>
      <BsArrowUp />
    </button>
  );
};

export default ScrollButton;
```

### Styling

Now that we coded the "crude" component, we can style it a little bit.

Add `styled-components`:

```javascript
yarn add styled-components
```

Or:

```javascript
npm i styled-components
```

Create the button and icon components:

```jsx
import React from "react";
import { BsArrowUp } from "react-icons/bs";
import styled from "styled-components";

const StyledButton = styled.button`
  position: fixed;
  bottom: 10vh;
  right: 6vw;
  cursor: pointer;
  background: #333;
  border: none;
  height: 30px;
  width: 30px;
  border-radius: 50%;
  align-items: center;
  justify-content: center;
`;
const StyledIcon = styled(BsArrowUp)`
  font-size: 1.5rem;
  color: #fff;
`;
```

After creating the `styled-components` we can apply the scroll helper functions to make the button only appear when the page is scrolled down:

First, we need to attach the state we created before, `scrolled`, on the styled button:

```jsx
return (
    <StyledButton onClick={scrollOnClick} $scrolled={scrolled}>
      <StyledIcon />
    </StyledButton>
  );
};
```

Then we use the state variable on the button component:

```jsx
const StyledButton = styled.button`
  display: ${({ $scrolled }) => ($scrolled ? "flex" : "none")};
  z-index: 999;
  position: fixed;
  bottom: 10vh;
  right: 6vw;
  cursor: pointer;
  background: #333;
  border: none;
  height: 30px;
  width: 30px;
  border-radius: 50%;
  align-items: center;
  justify-content: center;
`;
```

### Conclusion

Alright! The live example should be in front of you right now, as this blog has a version very close to this button that we coded.

The whole code should be this:

```jsx
import React from "react";
import { BsArrowUp } from "react-icons/bs";
import styled from "styled-components";

const StyledButton = styled.button`
  display: ${({ $scrolled }) => ($scrolled ? "flex" : "none")};
  z-index: 999;
  position: fixed;
  bottom: 10vh;
  right: 6vw;
  cursor: pointer;
  background: #333;
  border: none;
  height: 30px;
  width: 30px;
  border-radius: 50%;
  align-items: center;
  justify-content: center;
`;
const StyledIcon = styled(BsArrowUp)`
  font-size: 1.5rem;
  color: #fff;
`;

const ScrollButton = () => {
  const [scrolled, setScrolled] = React.useState(false);

  const scrollOnClick = () => {
    window.scrollTo(0, 0);
  };

  const handlePosition = () => {
    if (window.scrollY >= 200) {
      setScrolled(true);
    } else {
      setScrolled(false);
    }
  };

  React.useEffect(() => {
    window.addEventListener("scroll", handlePosition);

    return function cleanup() {
      window.removeEventListener("scroll", handlePosition);
    };
  }, []);

  return (
    <StyledButton onClick={scrollOnClick} $scrolled={scrolled}>
      <StyledIcon />
    </StyledButton>
  );
};

export default ScrollButton;
```

## Additional Resources

- [Github Repo](https://github.com/tsaristbomba/scroll-button-component)

- [HTML DOM element Object](https://www.w3schools.com/jsref/dom_obj_all.asp)

- [Window DOM](https://developer.mozilla.org/en-US/docs/Web/API/Window)

- [Styled Components](https://styled-components.com/)

- [React Icons](https://react-icons.github.io/react-icons)

- [React hooks](https://reactjs.org/docs/hooks-intro.html)
