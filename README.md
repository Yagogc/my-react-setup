# My React Setup

This repository is a collection of methodologies, snippets, components, configs so I can use them from project to project.

If you find this repository, go ahead and use whatever you see fit, but everything in here is catered for my personal use and is not intended to be a guide for anyone.

> ⚠️ NOTE: This repository is updated when I have the time to do it and is always being updated as I go along, so take everything with pinch of salt as many things could be outdated...

# Table of Contents

- [ESlint & Prettier](#eslint-and-prettier)
  - [Installation](#installation)
  - [package.json](#package.json)
  - [.eslintrc.json](#.eslintrc.json)
  - [.eslintignore](#.eslintignore)
  - [VS Code](#vs-code)
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

## ESlint & Prettier

### Installation:

```
$ npm install --save-dev eslint eslint-config-airbnb eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react prettier eslint-plugin-prettier eslint-config-prettier
```

### package.json

```
{
  "scripts": {
    "lint": "eslint .",
    "lintfix": "eslint . --fix",
    "precommit": "pretty-quick --staged"
  },
}
```

### .eslintrc.json

```
{
  "extends": ["airbnb", "plugin:prettier/recommended"],
  "env": {
      "browser": true,
      "jest": true
  },
  "rules": {
      "react/jsx-filename-extension": [1, {"extensions": [".js"]}]
  }
}

```

### .eslintignore

```
coverage/
```

### VS Code

To integrate it with VS Code, first install the following plugins:

- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- [ESlint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

Once they're installed, add the following to your user settings in VS Code:

```
# user-settings.json
{
  // Enables Prettier to format on save
  "editor.formatOnSave": true,
  "prettier.eslintIntegration": true,
}
```

Now when you save a file Prettier or ESlint should run and fix any format/lint error.

## Pre-commit

You can use ESlint/Prettier with a pre-commit tool. This can re-format your files that are marked as "staged" via git add before you commit.

### Installation:

```
$ npm install --save-dev husky pretty-quick
```

1. **husky**  - adds git hooks.
2. **pretty-quick**  - pre-commit hook for husky.

And add this config to your `package.json`:

```
#.eslintrc.json

"scripts": {
    "precommit": "pretty-quick --staged"
  }
```

Now, every time that any file is committed, Prettier will be executed on those files.

For more info about Prettier pre-commit click [here](https://prettier.io/docs/en/precommit.html).
