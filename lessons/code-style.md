---
path: '/code-style'
title: 'Adding a linter'
order: 5
section: 'Setup'
description: 'We talk about the importance of consistent code style and install a linter'
---

Adding a linter to your React Native project is a highly encouraged. Not only does it help ensure a consistent code style throughout the project, it also highlights errors and often uncovers bad practices. I always set up linting and code formatting from the onset when starting a new project, even if it's just personal or a hobby project!

The go-to linter for JavaScript is called [eslint](https://eslint.org/). There are three main reasons you should always install a linter:

1. **Enforce consistent code style** - double quotes or single? Trailing comma or no? Most experienced engineers have a preference one way or another, but ultimately most agree that it doesn't really matter, so long as it's consistent. With eslint we can set up these preferences once, and the whole project will be checked to ensure the same style is followed.
2. **Catch mistakes** - it's easy to miss typos, unused variables and forgetting to return a variable from a function while developing. When integrating eslint to your code editor, you'll get helpful warnings and errors for these issues while you're writing your code. Saves a lot of debugging time!
3. **Avoid bad practices** - JavaScript is a pretty amazing language in that it allows you to do pretty much anything. This is very powerful, but dangerous, because it leaves it up to us, the developers, to have some rules and order. Depending on the code style you do with (e.g. functional vs object oriented) there are many linting rules that help you enforce good practices that go with the code style you prefer.

## Adding eslint - installation (step 1 of 4)

First, we should install the package. For this, open your terminal, navigate to the root directory of your project and run the following:

With npm:

```sh
npm install eslint @react-native-community/eslint-config --save-dev
```

With yarn:

```sh
yarn add eslint @react-native-community/eslint-config --dev

```

This will add two packages to your dev dependencies:

- **eslint** - the code linter for JavaScript
- **@react-native-community/eslint-config** - a community-built eslint configuration for React Native

You can always configure your own linting rules of course, but I like to start with community presets.

## Adding eslint - adding the configuration files (step 2 of 4)

We've now installed both eslint and the community preset, but the eslint package doesn't know about the preset. In order to make eslint aware of this, we need to add a configuration file.

Create a new file in the root directory of your project and call it `.eslintrc.js` (yes, the filename starts with a `.`)

Open the file and add the following:

```js
// .eslintrc.js

module.exports = {
  root: true,
  extends: '@react-native-community',
};
```

This lets the linter know about the configuration package we want to use.

The community package actually comes with prettier pre-installed. Prettier is another package complimentary to eslint, but it focuses on code _formatting_. It mostly deals how the code looks rather than its correctness. The great thing about prettier is that if you can turn on "format on save" or have a pre-commit hook that runs its before a commit so your code will always be formatted uniformly.

Prettier has very few configuration options, because their mentality is to have as few variations as possible. I am definitely guilty of having a preference here. If you'd like your code to look exactly like mine in the example, add these prettier settings.

Create another file in the root directory of your project and call it `.prettierrc`

Open the file and add the following:

```js
// .prettierrc.js

module.exports = {
  bracketSpacing: true,
  singleQuote: true,
  trailingComma: 'all',
};
```

- `bracketSpacing` - adding a space around brackets, e.g. `import { useState } from 'react';` vs `import {useState} from 'react';`
- `singleQuote` - using single quotes for strings, e.g. `import React from 'react'` vs `import React from "react"`
- `trailingComma` - adding a trailing comma after array arguments (the default is not to have a trailing comma for the last element of the array)

## Adding eslint - adding the run script (step 3 of 4)

Now we have eslint installed and configured. But how to actually run it? Open the `package.json` in your project and add the following under the `scripts` section:

```json
"lint": "eslint ."
```

Now you can run `npm run lint` or `yarn lint` in your terminal and the linter will report both eslint and prettier issues.

## Adding eslint - adding it to your code editor (step 4 of 4)

It's all well and good to lint your code on the command line, but ideally you'd have instant feedback while you're writing your code. Thankfully most code editors have an integration option for this.

### VSCode

Code => Preferences => Extentions => ESLint

### Atom

Atom => Preferences => Install => linter-eslint

You may have to close and reopen your code editor for the package to start working, but that's it! You now have the optimal working environment.
