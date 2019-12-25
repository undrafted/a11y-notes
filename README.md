# a11y-notes

### 1. add `eslint-plugin-jsx-a11y`
```js
// example .eslintrc.json
{
  extends: [
    'plugins:jsx-a11y/recommended'
  ],
  plugins: ['jsx-a11y']
}
```

### 2. use `react-axe` library for auditing 

```js
// initialize react-axe before rendering the <App/>
if(process.env !== 'PRODUCTION'){

  const axe = requre('react-axe');
  const axeConfig = {
    rules: [
      {
        id: 'radioGroup',
        enabled: true
      }
    ]
  };
  
  // 1000ms - react-axe timeout before analysis after render
  axe(React, ReactDOM, 1000, axeConfig);
  }
  
 ReactDOM.render(<App/>, appId);
```

### 3. useful browser plugins for auditing
- `axe`
- `tota11y`
- `high contrast`

### 4. use your machine's voice-over a11y feature and try to navigate your webapp

### 5. define landmark regions (roles) 
- [a11yproject resource](https://a11yproject.com/posts/getting-started-aria/)

### 6. heading levels should convey structure of the page
- strictly use `h` tags for structure
- dont hesitate to use `p` and `span` tags for everything else

### 7. accessible labels
- wrap `input` elements with `label` if possible
- if not, use `for` and `id`
- more example: 
  instead of 
  ```js
  <Button>< back</Button>
  ```

  do: 
  ```js
  <Button aria-label="Go back to home page"><- back</Button>
  ```
- `aria-label` should be specific
- group connected parts of the page together so the screenreader can read them together. Example:
  
  instead of
  ```js
  <p>You are not logged in. <Link to="/login">Log in now</Login></p> 
  ```
  do:
  ```js
  <div aria-labelledby="not-logged-in log-in">
     <p id="not-logged-in">You are not logged in.</p>
     <Link to="/login" id="log-in">Log in now</Link>
  </div>
 
  ```

### 8. group input elements that are connected with each other (radio, select, etc)
- wrap in `fieldset`, add appropriate aria, etc

### 9. add accessible description to elements
- use `aria-describedby` in the `input` element pointing to the `id`s of the description elements. Example:

  ```js
  <input type="password" aria-describedby="password-requirement"/>
  <span id="password-requirement>Password must be at least 8 characters</span>
  ```
  
### 10. use meaningful img `alt` attributes
- don't hesitate to write `alt=""` if the image is decorative, so the screenreader can just skip the image
- when adding `alt` text, always consider the functionality the image provides, and if the information you would add for the `alt` is already present in another component next to it anyway (e.g. titles). Otherwise it would just be noise (and repetition) and would cause more harm than good.

### 11. define live region to ensure dynamic changes are announced to screen readers using arias (e.g submitting a form and getting an error feedback)

  - note that live regions should already be in the dom upon first render, so that screen readers can actually listen for their updates
  - note the aria-live assertive interrupts announcements, even other assertive elements before it!
  ```js
  // aria-live accepts two values: polite or assertive
  // polite waits for the screen reader to complete whatever it is reading before announcing the change
  // assertive will interrupt the screenreader to announce the change
  
  // aria-atomic tells the reader to present the element as a whole 
  // anytime any change is made even if only a part of the content changed
  
  // aria-relevant
  // accepts 'additions' 'removals' 'text' or all of them
  // additions - if any nodes are added
  // removals - if any nodes are removed
  // text - text change
  
  // values for aria-atomic and aria-relevant below are default values (no need to add, just added for explanation)
  <div id="error-span" aria-live="polite" aria-atomic="true" aria-relevant="additions text">
    Please enter a username.
  </div>

  ```
  
  ### 12. Approriately set focus on each page load
  - check page focus using `document.activeElement` upon navigation

### 13. use html5 sectioning elements if applicable, example:
  ```js
  // instead of 
  <div role="navigation">...</div>
  // do:
  <nav>...</nav>
  ```
