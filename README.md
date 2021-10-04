# Eslint config Jorn (for typescript)

This config gives you eslint configured with:  
- [standard js for typescript](https://standardjs.com/#typescript)
- [prettier](https://prettier.io/) without semicolons and with single quotes & trailing commas
- console and debugger statements are allowed in dev, but will throw when linted in your CI pipeline

## Setting up

```
npm install eslint-config-jorn-ts
```

Add `.eslintrc.js` to your project root..  
  
  ```js
  module.exports = {
    root: true,
    extends: 'eslint-config-jorn-ts',
  }
  ```

..and update `tsconfig.json` with:  
  
  ```json
  "include": [
    "./.eslintrc.js",
    "src"
  ]
  ```

Lastly, you may want to add a **package.json script** for linting the project. You can call this manually from the CLI or use it in your build pipeline to auto check your code.

```json
"scripts": {
  "lint": "eslint ./src"
}
```

## Editor integration

You want at least auto fix on save. To do this your editor needs to know what to do with the eslint config.

### VSCode

- Install extension [dbaeumer.vscode-eslint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- Add a settings file in your project root: `.vscode/settings.json` with:

```json
{
  "eslint.workingDirectories": [
    "./"
  ],
  "editor.defaultFormatter": "dbaeumer.vscode-eslint",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

## Issues

Not listed here? Let me know in the [repo](https://github.com/publicJorn/eslint-config-jorn-ts/issues)

### tsconfig not in project root

If your `tsconfig` file lives somewhere else (a subdir), you probably can't use package.json to connect. So add `.eslintrc.js` instead with:  

```js
module.exports = {
  root: true,
  extends: 'eslint-config-jorn-ts',
  parserOptions: {
    project: ['./<path_to>/tsconfig.json'],
  },
}
```

### Can I exclude stuff

Yes, just add an `.eslintignore` file. It has the same syntax as `.gitignore`.
