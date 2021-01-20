# How to fix Deploy directory 'build' does not exist Netlify

## Description

Build stage can surprise you with interesting and annoying bugs.

## Requirements

- Code editor
- Netlify
- Gatsby.js

## Introduction

As you are building a [Gatsby](https://www.gatsbyjs.com/) project, at a development point, you can encounter no errors whatsoever, but at a build stage, you can be surprised with one or many bugs that slip past through you.

## Problem

Let's say you successfully configure the [Netlify](https://www.netlify.com/) CLI and deploy your project. Then you get something like this in the **Deploys** section of the Netlify site page:

**Production**: master @id_number `Failed`

Then you look at the Deploy log:

```
    9:33:56 AM: Deploy directory 'build' does not exist
    9:33:56 AM: Failing build: Failed to build site
    9:33:56 AM: Failed during stage 'building site': Deploy directory 'build' does not exist
```

## Why does this happen?

The Gatsby project structure is different than let's say [React](https://reactjs.org/), that the build process **adds** a **build** folder. Gatsby builds the app for deployment in the **public** folder. So normally Netlify will try to find a **build** folder as a default configuration.

## Solution

To resolve this problem we have to find a way to make Netlify look for build files at the **public** folder instead.

Netlify has a way to edit the build settings, deploy settings, and environment variables (more information about that at the **Additional Resources section**) so we can fix those kinds of bugs easily.

Create a `netlify.toml` file at the root file of your project.

Populate the file as such:

```
[build]
    publish = "public/"
```

The publish setting is the one that can change the default build file for the Netlify build process. This is relative to the base directory.

## Additional Resources

- [Build file based config - Netlify ](https://docs.netlify.com/configure-builds/file-based-configuration/)
