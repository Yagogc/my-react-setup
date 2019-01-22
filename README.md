# My React Setup

This repository is a collection of methodologies, snippets, components, configs so I can use them from project to project.

If you find this repository, go ahead and use whatever you see fit, but everything in here is catered for my personal use and is not intended to be a guide for anyone.

> ⚠️ NOTE: This repository is updated when I have the time to do it and is always being updated as I go along, so take everything with pinch of salt as many things could be outdated...

# Table of Contents

- [ESlint](#eslint)
- [Prettier](#prettier)
- [Git Hooks](#git-hooks)
- [Unit Testing](#unit-testing)
  - [Jest](#jest)
  - [Enzyme](#enzyme)
- [E2E Testing](#e2e-testing)
  - [Cypress](#cypress)
  - [Pupeteer](#pupeteer)
- [CSS](#css)
  - [Styled Components](#styled-components)
  - [Emotion](#emotion)

## ESlint

> ESLint is an open source project to provide a pluggable linting utility for JavaScript. For more [info](https://eslint.org/)

I use ESlint in conjuction with the Airbnb rules.

### Installation:

```
$ npm install --save-dev eslint eslint-config-airbnb eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react
```

### NPM script

```
# package.json
{
  "scripts": {
    "lint": "eslint src",
    "precommit": "pretty-quick --staged"
  },
}
```

### Config

```
# .eslintrc
{
  "extends": ["airbnb"],
  "env": {
    "browser": true,
    "jest": true,
    "node": true
  },
  "rules": {
    "react/jsx-filename-extension": [1, {
      "extensions": [".js"]
    }],
    "react/no-unescaped-entities": 0
  },
  "parser": "babel-eslint"
}

```

### Ignore

```
# .eslintignore

coverage/
```

### VS Code

To integrate it with VS Code, first install the following plugin:

- [ESlint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

Now you should get live linting errors.

## Prettier

> Prettier is an opinionated code formatter. For more [info](https://prettier.io/)

I use prettier in conjunction with ESlint through _eslint-plugin-prettier_ and _eslint-config-prettier_.

[eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier): Runs Prettier as an ESLint rule and reports differences as individual ESLint issues.

[eslint-config-prettier](https://github.com/prettier/eslint-config-prettier): Turns off all the ESlint rules that are unnecessary or might conflict with Prettier.

### Installation:

```
$ npm install --save-dev prettier eslint-plugin-prettier eslint-config-prettier
```

### NPM script

```
# package.json
{
  "scripts": {
    "format": "npm run prettier -- --write",
    "prettier": "prettier \"**/*.+(js|jsx|json|yml|yaml|css|less|scss|ts|tsx|md|graphql|mdx)\"",
    "validate": "npm run lint && npm run prettier -- --list-different"
  },
}
```

### Config

```
# .prettierrc
{
  "semi": false,
  "singleQuote": true,
  "trailingComma": "es5",
  "tabWidth": 2,
  "useTabs": false
}

```

Also, to make prettier to play nice with ESLint we need to extend the eslint rules with "plugin:prettier/recommended" and "eslint-config-prettier"; like this:

```
# .eslintrc
{
  "extends": ["airbnb", "plugin:prettier/recommended", "prettier/react"],
  ...
}

```

### Ignore

```
# .prettierignore

package-lock.json
yarn.lock
node_modules
coverage
dist
build
.build
```

### VS Code

To integrate it with VS Code, first install the following plugi:

- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

Once is installed, add the following to your user settings in VS Code:

```
# user-settings.json
{
  // Enables Prettier to format on save
  "editor.formatOnSave": true,
  "prettier.eslintIntegration": true,
}
```

Now when you save a file Prettier should run and fix any format error.

## Git Hooks

You can run ESlint/Prettier with a pre-commit tool. This can re-format your files that are marked as "staged" via git add before you commit.

### Installation:

```
$ npm install --save-dev husky lint-staged
```

- [husky](https://github.com/typicode/husky): Git hooks made easy.
- [lint-staged](https://github.com/okonet/lint-staged): Run linters against staged git files.

And add this config to your `package.json`:

```
#.package.json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "pre-push": "npm test"
    }
  },
  "lint-staged": {
    "*.js": [
      "eslint"
    ],
    "**/*.+(js|jsx|json|yml|yaml|css|less|scss|ts|tsx|md|graphql|mdx)": [
      "prettier --write",
      "git add"
    ]
  },
  ...
}
```

Now, every time that any file is committed, Prettier will be executed on those files.

For more info about Prettier pre-commit click [here](https://prettier.io/docs/en/precommit.html).
