# The Ember Initiative Journey 🐹❤️

_Week 1 - the codemod_

Ember's power is to improve step by step. As the framework evolves, the community won't leave you behind: it will provide you with everything you need to update your app and adopt modern practices at your own pace. As usual, it will also help you migrate your classic Ember app to build with Vite. This is the first step of this journey: **a codemod to help developers migrate from classic apps to Vite apps**.

## A codemod?

A codemod is essentially a script that transforms your code automatically. In the Ember ecosystem, it's a widely used way to help developers adopt a new syntax. For instance, long ago, we wrote double-curlies syntax `{{#my-component}}` to invoke components in a template. Nowadays, we use the angle bracket syntax `<MyComponent>` instead. There is a [codemod that does this for you](https://github.com/ember-codemods/ember-angle-brackets-codemod), so if you need to migrate an old Ember app to the modern syntax, you don't have to do it all by yourself.

## How to approach a codemod?

To upgrade a classic Ember app to using Vite, we need to move, rename, and change a certain number of files. And since we want the new build system to work from `3.28` to the latest Ember (`6.x` when I am writing this), we expect to have many cases to handle. The task sounds overwhelming, so here are two approaches to start this:

### The happy path

Choose the _perfect_ use case, which could be a good starting point for transforming the code. Perfect can have different meanings depending on your context; for instance, it could mean "most standard". Regarding our classic-to-Vite codemod, the perfect case would be a brand-new empty app generated with `ember new` and initialized with the latest version of Ember. It means the app is completely up to date with modern practices and it doesn't have any customization, so it's the most basic case we want to handle, then we can keep building up out of it.

### The mirror

Once you have identified the perfect use case, look at it and look at what you want instead. Put the initial code and the result side by side to get a better picture of what you must achieve. In the present case, we are working at the scale of a whole application, so we can use a tool like [Beyond Compare](https://www.scootersoftware.com/). This software can compare entire folders; we can see what files exist on the left and the right, and by clicking on a file, we have the content diff. It's a very practical approach: you run your codemod on the left, you refresh Beyond Compare, and if there is no more diff, then you win. Combine this with `git` and a custom `reboot` command that reset the state of the left side to HEAD, and you have a good enough development workflow. 

<img width="1483" alt="codemod-story-compare" src="https://github.com/user-attachments/assets/0cd8b8af-4f5c-4892-9d6b-bb0cf85df16e" />

## Files creation

- Have a dep on Embroider app blueprint and use its files directly (babel config, vite config)
- Move index
=> The difference between the relative path and the path to codemod file (__dirname vs just ./)

## Addons meta

- about npm view
