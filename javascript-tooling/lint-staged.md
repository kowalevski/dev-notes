# Lint staged

You can lint and format by **eslint** and **prettier** git staged files in pre-commit action with module **lint-staged**

[[GitHub](https://github.com/okonet/lint-staged)]

Install dependency:

```bash
npm install --save-dev lint-staged
```

After that we need to configure file **.lintstagedrc** where we have to write our rules for specific files:

```json
{
  "*.+(js|ts|tsx)": [
    "eslint"
  ],
  "**/*.+(js|jsx|json|ts|tsx)": [
    "prettier --write",
    "git add"
  ]
}
```

You should already have **husky** in your project for running git actions. Now we should specify what we run lint-staged and other needed things in pre-commit action

**.huskyrc**

```json
{
  "hooks": {
    "pre-commit": "lint-staged && npm run build"
  }
}
```

### Running Jest git staged tests

If you're using **Jest** for testing your application, you can also run all git staged test files by **lint-staged**. For this you need to add a line "jest --findRelatedTests" in lint-staged configuration file:

```js
module.exports = {
  'src/**/*.+(js|jsx|json)': ['eslint'],
  '**/*.+(js|jsx|json|css|html|md)': [
    'prettier --write',
    'jest --findRelatedTests',
    'git add'
  ]
};
```

