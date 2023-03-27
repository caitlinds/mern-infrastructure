PT 3:

UPDATING STATE IN CLASS COMPONENTS:
- There’s two key differences in how state is updated in class vs. function components:
-- Class components always update state by invoking the inherited setState() method vs. invoking the setter function(s) returned by the useState hook in function components.
-- (useState hook was created to mimic setState() method)
-- setState() accepts an object as an arg and this object is merged into the existing state object.
-- This differs with how a function component’s setter function replaces that state with the value provided.
-- setState() is a method that a component inherits from the onstructor class
-- setState() merges object while setter fn in useState replaces object
HANDLING ONSUBMIT EVENT:
- The <form> React Element in <SignUpForm> already has an event handler method assigned to its onSubmit prop
- we need to prevent the form from being submitted to the server by including evt.preventDefault(); as the first line of code.

STYLE THE <SIGNUPFORM> CP:
- the <form> React Element has a className="form-container" prop
- The form-container CSS class is intended to be reused by multiple forms in the app, therefore it should be defined in the index.css module

ADD SERVICE AND API MODULES FOR THE CLIENT:
- Utility modules: Modules that hold general purpose functions, for example, a formatTime(seconds) function. These modules are reusable in multiple projects.
- Service modules: Service modules are where we can organize application specific logic such as functions for signing-up or logging in a user. Service modules often use and depend upon API modules…
- API modules: API modules are for abstracting logic that make network requests such as AJAX calls to the backend or third-party APIs. This abstraction makes it easier to refactor code to use different techniques, libraries, etc. For example, we are going to be using fetch for our AJAX communications, however, refactoring to use a library such as Axios would be made easy thanks to the use of API modules.
-- AJAX calls, holds back-end coding, tokens, etc
- mkdir src/utilities
-- hold any utility, service or API modules that we need in the future
- touch src/utilities/users-service.js
-- organize functions used to sign-up, log in, log out, etc.
- touch src/utilities/users-api.js
-- make AJAX requests to the Express server
-- create an API module that will handle user-related communications with the server

PT4:
Implementing Token-Based Auth:

REVIEW OF FETCH:
- promise-based, meaning fetch API will return promise that resolves to promise object
- .then is used to access resolved promise 
- resPromise.then(res => console.log(res))
-- response obj returned
-- ok property confirms successful fetch
- .then() also returns promise itself, allowing chaining (.then.then())
- The JSONPlaceholder API, like most APIs, responds with JSON data (content-type: application/json header)
- If the response object has JSON data in its body, the json() method is used to retrieve the data:
> let dataPromise = resPromise.then(res => res.json());
< undefined
-- first promise is repsone obj, second promise when we call JSON on response object
-- so we must call .then again
> dataPromise.then(data => console.log(data));
  (10) [{…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}]
< Promise {<pending>}
-- can just do console.log bc it will pass in data since conole.log is cb fn

REVIEW OF HANDLING PROMISES W ASYNC/AWAIT:
- The await keyword essentially “pauses” the code until the promise is resolved and causes the promise to return its resolved value allowing us to assign the value to variables
- In order to use the magical await keyword, we must preface its containing function with the async keyword
- used to fetch API data asynchronously and render synchronous code while it returns its value

MAKE THE AJAX REQUEST TO SIGN-UP:
- the state in <SignUpForm> is ready to be sent to the server via AJAX
- fetch requests will be defined outside of cps, in service module
- preventDefault() prevents form from being sent to server and resulting in full page re-load
    USE TRY/CATCH BLOCK TO CATCH ERRORS WHEN USING ASYNCH/AWAIT:
- when using a/a we cant use .catch to handle errors
- must mark fn as asynch so we can use await
- error message rendered at bottom of render fn
    try {
      
    } catch {
      // An error occurred 
      this.setState({ error: 'Sign Up Failed - Try Again' });
    }
  };
- Ready the Sign Up Data Payload
- There are two extra properties on the state object we don't want to send to the server 
-- state.confirm and state.error
- .setState always used to update state in class cps!
- Make a New Object Called "formData" Containing Just the Three Properties:
-- destructue state obj
-- make new formData variable with only 3 properties server needs
    try {
      const {name, email, password} = this.state;
      const formData = {name, email, password};
    }
- put sign up related app logic in the users-service.js service module and network logic in the users-api.js API module 
    FOLLOW THE CODING FLOW:
- SignUpForm.jsx <--> users-service.js <--> users-api.js <-Internet-> server.js (Express)
-- business logic: users-service: save a token in local storage, handle case when token expires, extracting user info (from data payload) from token, etc
-- users-api: AJAX requests logic: handles AJAX communication in reference to user data resource
-- server: routes, controllers, etc
-- future: orders-api: get user previous orders, etc
-- SignUpForm wants user info to update state
- in app, we have user, and setUser state defined
-- signupform will want user info
- users-service will want token from users-api which will get from server
- we will often call fns and methods that dont exist yet 
-- see users-api
-- see users-whatever

DEFINE THE SERVER-SIDE ROUTE FOR SIGNING UP:
- 
