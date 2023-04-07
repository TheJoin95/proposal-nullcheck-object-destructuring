# Proposal of null check object destructuring

Proposal to add the null check in objct destructuring syntax

## Status

State: -1

Author: @thejoin95 ([@thejoin95](https://twitter.com/thejoin95))

Champion: need one

## Motivation

Object destructuring is well use by the javascript developers. The default value in case of an undefined prop is useful and I think it could be even better if we are going to implement it as well with the null check, especially for a nested object in order to avoid null check errors.

## Use cases & description

Imagine to have an object with n depth level, e.g. a react state/context with differents properties containing n-depth objects.
In some scenario you want to destructure few properties at the first level and in other case also some more specific in-depth props.

```
const state = {
  navbar: {
    profileMenu: {
      username: 'jhondoe',
      ...
    }
  },
  footer: {
    brand: {
      title: 'brand one',
      ...
    }
  },
  ...
}

const {
  navbar: {
    profileMenu: {
      username: ProfileMenuUsername
    }
  }
} = state;

```

Let's say that, the properties are going to be valorised but some of them would have a `null` value:

```
{
  navbar: {
    profileMenu: null,
  },
  footer: {
    brand: {
      title: 'brand one',
      ...
    }
  },
  ...
}

const {
  navbar: {
    profileMenu: {
      username: ProfileMenuUsername
    }
  }
} = state; // this will break because there is no valid username prop in null

```

When a nested property is undefined, we could assign the default value, defined in the object destructuring syntax:

```
const {
  navbar: {
    profileMenu: {
      username: ProfileMenuUsername
    } = { username: null }
  } = { profileMenu: { username: null } }
} = state;

```

It would be great to have a syntax to indicate whenever a property could be nullable by adding a short circuit instead of throwing an error by reusing the `.?`, such like:

```
const {
  navbar: {
    profileMenu?: {
      username: ProfileMenuUsername
    } = { username: null }
  } = { profileMenu: { username: null } }
} = state;

```

## Comparison

These npm modules do something like the proposal:
- [lodash.get](https://lodash.com/docs/#get)

Even though is a different approach, would say old style, and I believe it should implemented directly on the destructure syntax.

## Q&A

In progress