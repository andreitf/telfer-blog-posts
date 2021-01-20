# How to properly map array items in React

## Description

Doing an array map in jsx is not that intuitive, it seems. Let's learn how to do it properly.

## Requirements

- Code editor
- React.js

# Introduction

While building a [React](https://reactjs.org/) app we might have to do some array mapping, and then some problems may occur.

## Code

A typical arrow function is called as such:

```javascript
const arrowFunction = () => {
  // do something
};
```

By that logic in `jsx` you would do something like this, right?

```jsx
const arrowFunction = () => {
  <h1>Hello World</h1>;
};
```

Wrong! there's something you are forgetting that will make you feel a little stupid 😅, the function needs to return something, so in `jsx` we need to return the markdown as well.

So in a mapping scenario:

```jsx
const data = ["a", "b", "c", "d"];

const TypicalComponent = () => {
  return (
    <div>
      <h1>Hello World</h1>
      {data.map((item, key) => {
        return <h2>{item}</h2>;
      })}
    </div>
  );
};
```

We can even simplify:

```jsx
    {data.map(item, key) => <h2 key={key}>{item}</h2>}
```

Or if you have several items:

```jsx
    {data.map(item, key) => {
        return (
            <React.Fragment>
                <h1>{item.title}</h1>
                <ul>
                    <li>{item.list}</li>
                </ul>
            </React.Fragment>
        )
    }}
```

## Additional Resources

- [React Lists and Keys](https://reactjs.org/docs/lists-and-keys.html)
