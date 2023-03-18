### Table of Content
* <a href="https://beta.reactjs.org/learn">Docs React.js org</a>
* <a href="#setup-requirements">Setup</a>
* <a href="#commands">Commands</a>
* <a href="#create-react-app">Create React App</a>
* <a href="#project-structure">Project Structure</a>
* <a href="#basic-terminology">IMP terms</a>

### Setup requirements:
* Node 
* NPM
* Code editor
* Browser

### Commands
#### Create React App:
  `npx create-react-app appname`<br/>
  **NPX** temporarily downloads the **create-react-app** and using it our app is created. Then **create-react-app** packge is deleted.<br/><br/>
  `npm start`<br/>
  Starts the app

### Project Structure
* **package.json**
  * contains project information and required packages for the project.
* **package-lock.json**
* **node_modules**
  * Contains all the downloaded packages 
* **public**/
  * contains index.html and other publically available resources for the project.
* **src**/
  * Contains all components of the project.
### Basic Terminology
* **Components**
  * Building blocks of a react app.
* **Props** 
  * (Properties) passed to the components, just like parameters to a function.
* **Strict Mode**
  * Checks for common bugs in react app and shows warnings in the console. It's Good to use it in our app.
* **JSX**
  * JSX (JavaScript Syntax Extension and occasionally referred as JavaScript XML) is an extension to the JavaScript language syntax. It is similar in appearance to HTML. It allows one to write HTML+JS together. 
  * We use `className` in JSX while `class` in HTML. This is because in JS `class` is a reserved keyword, so can't be used for element/tags names.
  * `for` is also a reserved keyword, so we need to use `htmlFor`
### Building 
**src/index.js** renders the given component (usually App.js component) in the **public/html**'s root div. We add everything in the App component only, and create new components.
React prefers camelCase.
