# Add Prettier to Your Project

- Add prettier vscode extension

- Install neccessary packages as dev dependencies

  ```js
  npm install -D prettier eslint-config-prettier eslint-plugin-prettier
  ```

- Add .prettierrc.js config file

  ```js
  module.exports = {
    semi: false,
    trailingComma: 'es5',
    singleQuote: true,
    printWidth: 80,
    tabWidth: 2,
    endOfLine: 'auto',
  };
  ```

- Update eslint config file if needed

  - Add these 2 lines to `extends : []`

    ```js
    extends: [
    'prettier/@typescript-eslint',
    'plugin:prettier/recommended'
    ]
    ```

- Add format script to package.json

  ```js
  "format": "prettier --write \"./src/**/*.{js,jsx,ts,tsx,json,css,scss,md}\""
  ```
