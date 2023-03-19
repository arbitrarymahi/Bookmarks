### Table of Content
* <a href="https://beta.reactjs.org/learn">Docs React.js org</a>
* <a href="#setup-requirements">Setup</a>
* <a href="#tips">Some Tips</a>
* <a href="#commands">Commands</a>
* <a href="#create-react-app">Create React App</a>
* <a href="#project-structure">Project Structure</a>
* <a href="#default-vs-named-exports">Default vs Named exports</a>

<details>
  <summary>Setup requirements</summary>
  
### Setup requirements:
* Node 
* NPM
* Code editor
* Browser

  </details>
### Commands
#### Create React App:
  `npx create-react-app appname`<br/>
  **NPX** temporarily downloads the **create-react-app** and using it our app is created. Then **create-react-app** packge is deleted.<br/><br/>
  `npm install`<br/>
  installs all the modules inside package.json<br/><br/>
  `npm start`<br/>
  Starts development build of the app<br/><br/>
  `npm run build`<br/>
  create a production build of the app
  
### Tips 
* **src/index.js** renders the given component (usually App.js component) in the **public/html**'s root div. We add everything in the App component only, and create new components.
* React prefers camelCase.
* Keep things organized from start by segregating in respective directories.

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
  * Names start with capital letter
* **Props** 
  * (Properties) passed to the components, just like parameters to a function.
* **Strict Mode**
  * Checks for common bugs in react app and shows warnings in the console. It's Good to use it in our app.
* **JSX**
  * JSX (JavaScript Syntax Extension and occasionally referred as JavaScript XML) is an extension to the JavaScript language syntax. It is similar in appearance to HTML. It allows one to write HTML+JS together. 
  * We use `className` in JSX while `class` in HTML. This is because in JS `class` is a reserved keyword, so can't be used for element/tags names.
  * `for` is also a reserved keyword, so we need to use `htmlFor`
  * We can return only one element. To return more than one element, we can wrap all in JSX Fragment **<>...</>**
  * we can use JS variables inside curly braces. ex: `{var_name}`

### Default vs named exports
we can export variables, functions classses etc using `export` keyword.
* Default export use the default keyword.
* There can be only one default export per module.
* Default exports can be imported using any name/alias in importing module.
```
exportmodule.mjs:
export default x;
------------------------------------
importmodule.mjs:
import axe from './exportmodule.mjs';
console.log(axe);
```
* named module are imported and exported using curly braces {}.
* They must be imported using their original(exported) name.
* We can have any number of named exports in a module.

```
exportmodule.mjs:
export {x};
export {y};
------------------------------------
importmodule.mjs:
import {axe,why} from './exportmodule.mjs'; //wrong, can't alias to some other name
import {x,y} from './exportmodule.mjs'; //correct
console.log(x);
```
### Props
#### passing props
* We can pass the props inside tags of the component, where we use the component
* Ex : `<My_Component title="my_title" prop2 = "something here" />`
* Then inside the component itself, we can use them just like function arguments. 
* Props are read-only, inside the components, they should only be used and not overwritten.(pure function)

#### proptypes and default props
* We can define the expected type of the props inside a component by using `component.propTypes` property of the component.
* We need to `import PropTypes from prop-types`
* We can also use `isRequired` to set a prop as required.(it's good to ensure this)
* `ComponentName.propTypes = { firstProp : PropTypes.string, secondProp : PropTypes.string.isRequired ...}`
* using defaultProps we can set default values.
* `ComponentName.defaultProps = { firstProp : 'value 1', secondProp : ...}`
