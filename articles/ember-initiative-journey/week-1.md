# The Ember Initiative Journey 🐹❤️

_Week 1 - the codemod_

Ember's power is to improve step by step. As the framework evolves, the community won't leave you behind: it will provide you with everything you need to update your app and adopt modern practices at your own pace. As usual, it will also help you migrate your classic Ember app to build with Vite. This is the first step of this journey: **a codemod to help developers migrate from classic apps to Vite apps**.

## A codemod?

A codemod is a script that transforms your code automatically. In the Ember ecosystem, it's a widely used way to help developers adopt a new syntax. For instance, long ago, we used to write components with the double-curlies syntax `{{#my-component}}` to invoke components in a template. Nowadays, we use the angle bracket syntax `<MyComponent>` instead. There is a [codemod that does this for you](https://github.com/ember-codemods/ember-angle-brackets-codemod), so if you need to migrate an old Ember app to the modern syntax, you don't have to do it all by yourself.

## The approach

- Happy path, ember-cli up to date
- Create a classic app with ember new
- Create a vite app with Embroider app blueprint
- Use a tool like beyond compare
=> when we call the codemod, classic app should become the same as vite app

## Files creation

- Have a dep on Embroider app blueprint and use its files directly (babel config, vite config)
- Move index
=> The difference between the relative path and the path to codemod file (__dirname vs just ./)

## Addons meta

- about npm view
