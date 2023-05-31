REACT FUNDAMENTALS:

COMPONENTS:
- Components are the building block of User Interfaces and are fundamental to today’s front-end libraries/frameworks, including React, Angular & Vue.
- Let’s contrast the two different kinds of components in React:
-- User-defined components that we as developers define
-- Built-in components that are part of the React library

USER DEFINED COMP0NENTS:
- We code user-defined components and use them to compose the application’s user interface
- Our user-defined components typically render other user-defined components and/or React’s built-in components
- *User-defined components themselves, e.g., <App> do not render an HTML element in the DOM
-- a browser wouldn’t know what an <App> HTML element is.

REACT ELEMENTS:
- React Elements are components built into React
- A React Element exists for each HTML element we’re familiar with and thus, are easily recognizable in the JSX
-- ie <div>, <ul>, <li>, etc
- When a React Element is rendered, its corresponding HTML element will be created in the page (DOM)

HTML/CP HIERARCHY:
- In a React app, the tree-like hierarchy of the HTML elements in the browser document is a result of a hierarchy of components being rendered
- At the top of that component hierarchy is, by convention, a user-defined component named <App>

HOW A REACT APP IS LOADED AND RENDERS:
- Here’s what happens when a user browses to a web app that uses React for its front-end UI:
1) User browses to web app
2) Web app serves single index.html to browser
3) A <script> tag in index.html loads the React app's JS
-- this JS that's loaded is the React app (React is 100% JS)
4) The JS executes beginning at the entry point specified in package.json (typically index.js)
5) root.render (<App/>); The root element in index.js renders the top-level cp (typically <App/>)
6) When any cp is rendered, its children are rendered as well
7) A cp re-renders when state is updated
-- UI remains static until state changes

HIGH PERFORMNACE RENDERING OF CPS:
- React:
1) Renders all React Element components into a Virtual DOM.
2) After all components have been rendered, React compares the current Virtual DOM to the previous Virtual DOM and computes what is called the “diff”.
3) React uses the “diff” to make only the necessary changes to the actual DOM in the browser.

REVIEW:
- True or False: A Function Component is a component that is written as a JS function and returns its user interface as JSX.
-- True

DESIGNING UI'S USING CPS:
- 