# The Ember Initiative Journey 🐹❤️

_Week 2 - releasing the codemod_

_#web #emberjs #codemod #docs #embroider #vite #vitest_

At the end of this second week, we have the first release of [ember-vite-codemod](https://www.npmjs.com/package/ember-vite-codemod)! It can make Ember >=5.12 apps building with Vite. Aside from all the AST manipulations, I had the opportunity to have a clearer vision of where we are going with this.

## Do or document

As defined last week, a codemod is a script that transforms your code automatically. To put it differently, let's assume that you document entirely the way the code should be transformed: a codemod is like a script that automatically follows your docs so your users don't have to follow it themselves. But as long as the docs exist, the codemod is just a bonus with two purposes: saving your users time and protecting them from a feeling of overwhelm that could turn them away from your lib.

With this idea in mind, it's up to you to put the cursor on what your codemod can or cannot do; What is part of its job? What should remain the responsibility of the developer running it?

In the case of ember-vite-codemod, a relevant example might be the linter configuration _versus_ the new Babel config. A pattern in some legacy Ember apps is to have `@babel/plugin-proposal-decorators` installed and configured in the `eslint.config.mjs`: 
```
requireConfigFile: false,
babelOptions: {
  plugins: [
    ['@babel/plugin-proposal-decorators', { decoratorsBeforeExport: true }],
  ],
},
```
Whereas in a new Embroider+Vite app, the dependency `decorator-transforms` is used in the new Babel config `babel.config.cjs`. Suppose the pattern above is present in the Ember app and you run the codemod, then the linter will throw a parsing error "Cannot use the decorators and decorators-legacy plugin together".

But do we want to do something about it? The answer turns out to be no. The purpose of the codemod is to get the app building with Vite. The linter configuration is not related to the build; it's the developer's responsibility, so we prefer _document_ over _do_.

## The way back to Ember 3.28

I implemented the first iteration of the codemod using a freshly generated Ember 6.2 app. But we want Ember 3.28 apps to build with Vite, so we need a strategy to go all the way back. This part of the work has been the main focus for my colleague Chris Manson; to achieve this, we used tests and CI.

The idea is that we have a CI job that runs a vitest test called [`all-versions.test.js`](https://github.com/mainmatter/ember-vite-codemod/blob/main/tests/all-versions.test.js). This test:
- Generates a new Ember app for each Ember version we want to support.
- Creates an acceptance test so that when the app tests run, it builds and visits the home page.
- Runs the tests to check they pass when the app builds with Broccoli.
- Runs the codemod.
- Runs the tests once more to check they still pass now that the app should build with Vite.

All the versions we _want to support_ are commented, and all the versions we _do support_ are run:
```
const testVersions = [
  // ['ember-cli-3.28'],
  // ['ember-cli-4.12'],
  // ['ember-cli-4.4'],
  // ['ember-cli-4.8'],
  // // test helpers seems to be broken for most ember versions 😭
  // ['ember-cli-5.4', ['@ember/test-helpers@latest']],
  // ['ember-cli-5.8', ['@ember/test-helpers@latest']],
  ['ember-cli-5.12', ['@ember/test-helpers@latest']],
  ['ember-cli-latest'],
];
```

<br />
<br />

_Having the first version of the codemod released is a great achievement for this week. Now that we plan to communicate about it, we may have issues reported by the community. Also, there is one case we want to "do over document", which is the apps building with @embroider/webpack. It might be my focus next week._

<br />
[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md)
[Week 1](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-1.md)
[Week 3](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-3.md)
