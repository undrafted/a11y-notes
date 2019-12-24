# a11y-notes

### 1. add eslint-plugin-jsx-a11y
```js
// example .eslintrc.json
{
  extends: [
    'plugins:jsx-a11y/recommended'
  ],
  plugins: ['jsx-a11y']
}
```

### 2. `react-axe` for auditing

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

### useful browser plugins for auditing
- `axe`
- `tota11y`
- `high contrast`
