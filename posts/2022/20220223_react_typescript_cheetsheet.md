---
title: React + Typescript cheatsheet
author: Snehesh
tags: react, typescript, cheatsheet, jsx
link: /react-typescript-cheetsheet
published: false
created: 2022-02-23T15:06:02Z
modified: 2022-02-23T15:06:02Z
---

# React + Typescript cheatsheet

## Setup

If you use [atom](https://atom.io/)... download & install the following packages:
* [atom-typescript](https://atom.io/packages/atom-typescript)
* [linter-tslint](https://atom.io/packages/linter-tslint)


## What are Typescript type definition files? (*.d.ts)
You may see a folder called `typings` with a lot of files that follow the pattern `*.d.ts`. These are type definition files. Type definition files are used to declare the [interfaces](#interface) of public API of third party libraries like [jQuery](https://jquery.com/) or [React](https://facebook.github.io/react/). That way you don't have to create all the typings for third party libraries!

## How do you create a React component with Typescript?
* Create a file using the `.tsx` extention

* Declare the [interface](#interface) for any props that that the React Component uses
```javascript
interface TodoProps {
    todo: string
    status: string
}
```

* Declare the [interface](#interface) for any state that exists within the React component
```javascript
interface TodoState {
    isEditing?: boolean
    // Make all state optional! See Hack below
}
```
**Hack**: For now make every key in state optional or else Typescript with throw an error

* Create a React component using the interfaces you created
```javascript
class TodoComponent extends React.Component<TodoProps, TodoState> {
    constructor(props: TodoProps) {
        super(props)
        this.state = { ... } // initial state
    }
    ... // public + react methods
}
```

## Misc

### refs
In order for Typescript to be happy, use refs inside the class like so:
```javascript
class Cat extends <CatProps, {}> { // no state
  refs: {
    [key: string]: (Element)
    litterBox: (HTMLInputElement) // !important
  }
  constructor(props: CatProps){ ... } // constructor
  render() {
    return (
      <div ref="litterBox">
        litter
      </div>
    )
  }
}
```

## Glossary

### Interface
A collection of types that describes the *shape* that a value must have

```javascript
interface CatValue {
  name: string
  age: number
}

function petCat(cat: VatValue) {
  console.log(cat.name)
}

let myCat = { name: 'Whiskers', age: 4 }
petCat(myCat) // 'Whiskers'
```

**PROTIP**: use `?` for optional values
```javascript
interface CatValue {
  name: string
  age: number
  favoriteFish?: string // optional
}
```
