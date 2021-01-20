# How to handle loading in React

## Description

Loading it's a very important function of an app that requires outside data, authentication, etc.

## Requirements

- Code Editor
- React.js

## Introduction

Let's then code a Loading in a hypothetical authentication scenario, so when the component loads the Loading function gets called.

## Code

Let's say we have this scenario:

```jsx
const [isAuthenticated, setIsAuthenticated] = useState();

const handleAuth = async () => {
  const res = await authenticate();
  setIsAuthenticated(res.data.auth);
};

useEffect(() => {
  handleAuth();
}, []);
```

While the `handleAuth` is working we have to make a way to output that into the `jsx`

Start with creating a state:

```jsx
const [isAuthenticated, setIsAuthenticated] = useState();
const [loading, setLoading] = useState();

const handleAuth = async () => {
  setLoading(true); // start loading

  const res = await authenticate();
  setIsAuthenticated(res.data.auth);

  setLoading(false); // ends loading
};

useEffect(() => {
  handleAuth();
}, []);
```

Now we put the loading state to use:

```jsx
const [isAuthenticated, setIsAuthenticated] = useState();
const [loading, setLoading] = useState(true);

const handleAuth = async () => {
  setLoading(true); // start loading

  const res = await authenticate();
  setIsAuthenticated(res.data.auth);

  setLoading(false); // ends loading
};

useEffect(() => {
  handleAuth();
}, []);

return <div>{loading ? <h1>Loading...</h1> : <h1>Loaded</h1>}</div>;
```

## Additional Resources

- [React Hooks Documentation](https://reactjs.org/docs/hooks-intro.html)
