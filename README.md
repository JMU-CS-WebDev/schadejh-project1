# GitHubber

Get some more practice with react apps with [remote state](https://allover.twodee.org/remote-state/state-management-meets-web-services/).

## Task 0

Creating a frontend client for the Unforget would be helpful for further work with react, redux, and remote state (via thunk). It's a bit involved. If you haven't had a chance to do it yet, please make time ASAP so that you can get your questions answered before you're trying to apply this to your own Project.

## Task 1

<p>Your task is to write a React/Redux app that shows GitHub repositories matching a query. The matches will be provided by GitHub’s REST API. The end product will look something like this:</p>

<img src="https://twodee.org/gray/webdev/2021c/21-githubber/sample.png" style="border: 1px solid black;">

### Start from the Template

Clone your repo from the corresponding GitHub Classroom Assignment.

That template has already accounted for these steps:

#### Already in the GH Clasroom Repo

<p>In the terminal, create a new React app and move into its directory:</p>

<pre>npx create-react-app githubber
cd githubber
npm install redux react-redux redux-thunk</pre>

#### Continue with these steps

<p>The next three sections can be done in parallel. Split them up between team members.</p>

<h3>Store</h3>

<p>Create <code>store.js</code> as was done in the reading. Define a reducer that accepts the current state and an action and yields the new state. For the moment, the reducer should not do anything interesting. Whatever the action, return the unmodified state.</p>

<p>For initial testing, prime your state with a structure like this:</p>

<pre>
const initialState = {
  matches: [
    {
      full_name: 'JMU-CS-WebDev/fiction',
      description: 'This repository does not exist.',
      html_url: 'https://github.com/JMU-CS-WebDev/fiction',
    },
  ],
};
</pre>

<p>Define a store using the reducer, this initial state, and the <code>thunk</code> middleware.</p>

<h3>Provider</h3>

<p>In <code>index.js</code>, add a <code>Provider</code> component and pass your store as a prop.</p>

<h3>Repository</h3>

<p>Define a <code>Repository</code> component in <code>Repository.js</code>. It receives a prop named <code>repository</code>, which is an object shaped like the example from the initial state shown above, having keys <code>full_name</code>, <code>description</code>, and <code>html_url</code>. Display the repository’s full name in an anchor tag and the repository’s description.</p>

<h3>App</h3>

<p>Your next task is to reach into the global store and turn its <code>matches</code> array into viewable components. Complete the following steps in <code>App.js</code>.</p>

<ul>
  <li>Use the <code>useSelector</code> hook to grab the matches from the store.</li>
  <li>Map each match to a <code>Repository</code> component. You should see the initial state showing <code>JMU-CS-WebDev/fiction</code>.</li>
</ul>

<p>Next add a search box so the user can query for real repositories. Follow these steps:</p>

<ul>
  <li>Add a text input for the query.</li>
  <li>Add local state to hold the query text.</li>
  <li>Add a button to fire off the query.</li>
  <li>Add a callback for the button that dispatches a <code>startSearching</code> action (defined elsewhere).</li>
</ul>

<h3>Actions</h3>

<p>Now that you’ve got the initial state showing, it’s time to add some actions to pull down new state from GitHub’s REST API. Complete the following steps.</p>

<ul>
  <li>Create <code>actions.js</code>. It will have a structure similar to the ones from the readings.</li>
  <li>Add an object named <code>Action</code> that acts as an enum. Give it an entry for <code>LoadMatches</code>.</li>
  <li>Add an action creator named <code>loadMatches</code> that accepts an array of matches as a parameter. Have it return an object whose <code>type</code> is <code>Action.LoadMatches</code> and whose <code>payload</code> is the array of matches.</li>
  <li>Add a thunk creator named <code>startSearching</code> that accepts a query string. It returns a lambda that accepts the dispatch function and fetches a list of repositories that match the query. Use the URL <code>https://api.github.com/search/repositories?q=QUERY</code>, replacing <code>QUERY</code> with the actual query string.</li>
  <li>Interpret the fetched results as JSON. The JSON has the structure specified under <em>Default Response</em> in <a href="https://docs.github.com/en/free-pro-team@latest/rest/reference/search#search-repositories" target="_blank" rel="noopener">this endpoint’s documentation</a>. You can also see what is fetched by pasting the URL in your browser’s location bar.</li>
  <li>Once the JSON is parsed, dispatch a <code>loadMatches</code> action, passing in the matching repositories.</li>
  <li>In your reducer, add a case for <code>Action.LoadMatches</code>. Return a new state whose <code>matches</code> property is the action’s payload.</li>
</ul>

<p>When the user types in a query and hits the button, the fetch will update the store and automatically re-render the app and display the matching repositories.</p>

## Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

### Available Scripts

In the project directory, you can run:

#### `yarn start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

#### `yarn test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

#### `yarn build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

#### `yarn eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

### Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

#### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

#### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

#### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

#### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

#### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

#### `yarn build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
