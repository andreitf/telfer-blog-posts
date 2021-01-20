# How to fix Yarn Error: EPERM: operation not permitted.

If you stumbled upon this error there some ways we can go about solving it.

## Requirements

- Code Editor
- Windows 10

## What solved to me

### Corrupted node_modules folder

I had this error pop to me during coding a [Gatsby](https://www.gatsbyjs.com/) project, I just saved some file and realized that I needed a certain library, tried to install it with the usual:

```
yarn add some-library
```

and there it was, the unfortunate error:

```
yarn add some-library`
Yarn Error: EPERM: operation not permited, unlink "..."
```

So upon some research I decided to delete node_modules folder, a pretty common way to solve local errors. Go to the folder that you project is hosted, then:

```
rmdir /s node_modules
```

then install all dependencies again:

```
rmdir /s node_modules
yarn install
```

### Update your `yarn` version

What also might be a good idea is to update your `yarn` version. Some bugs may appear also after stable versions of programs, so it is a possibility that could happen with these types of bugs.
So to update Yarn on Windows you can use `choco`:

```
choco upgrade yarn
```

While `choco` is the recomended way to update `yarn`, you also can install via `npm` like so:

```
npm install -g yarn
```

## Additional information

- [`yarn` documentation](https://classic.yarnpkg.com/en/docs)

- [`npm` documentation](https://docs.npmjs.com/)
