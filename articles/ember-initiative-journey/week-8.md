# The Ember Initiative Journey 🐹❤️

_Week 8 - a new release for ember-test-selectors_

_#web #emberjs #embertestselectors #pnpm #workspaces #babel #viteplugins #rollupplugins #emberinspector_

[ember-test-selectors 7.1.0](https://github.com/mainmatter/ember-test-selectors/releases/tag/v7.1.0-ember-test-selectors) is out, along with **strip-test-selectors 1.0.0**. After this topic was closed, I could also look into some issues on ember-vite-codemod and pair with Chris on our big next step: getting Ember Inspector work with Vite.

## Tips from ember-test-selectors

### About `workspace:*`

ember-test-selectors is now a monorepo with the following structure:

- ember-test-selectors: the classic addon that used to exit before
- strip-test-selectors: the transform functions you can configure in your Babel config directly when your app uses Embroider+Vite
- tests:
  - classic-app: tests the compatibility of the classic addon
  - node-tests: unit tests for the plugin that strip `data-test-*` from JS objects
  - vite-app: tests the configuration for strip-test-selectors 

Working with monorepos requires familiarity with the concept of [workspaces](https://docs.npmjs.com/cli/v7/using-npm/workspaces). To simplify the idea, it's a protocol that allows you to declare what are the different packages contained in your monorepo.

If you have already looked into a v2 addon monorepo relying on pnpm, you may have seen the syntax `"my-v2-addon": "workspace:*"` in the `package.json` of the test app. This syntax means "please use the local version of `my-v2-addon`, whatever it is", so you don't need to manage a manual version update inside a monorepo. 

What you may not be aware of, though, is that this concept is something pnpm calls [workspace aliases](https://pnpm.io/workspaces#referencing-workspace-packages-through-aliases), and there is something very important to know about it: the workspace aliases are interpreted and replaced during the `pnpm publish`. It means that as long as you use `pnpm publish` to publish your public packages, you can safely use `workspace:*` inside a public package that depends on another package of the monorepo (e.g. ember-test-selectors [has a dependency](https://github.com/mainmatter/ember-test-selectors/blob/master/ember-test-selectors/package.json#L18) on strip-test-selectors).

### Using Babel in a Vite app

The new documentation for strip-test-selectors explains how to configure Babel in your Embroider+Vite app to reproduce the behavior of the classic addon. If you have an Embroider+Vite app, you necessarily have an existing `babel.config.cjs` file already. This is a requirement because any fresh empty Embroider+Vite app relies on Babel plugins out of the box, this is part of the app blueprint.

Have you ever wondered how the `babel.config.cjs` ends up being used, though? If you generate a simple Vite app using `pnpm create vite`, it won't use Babel out of the box; you need a way to tell Vite that Babel has to be executed at some point. The answers lie in `vite.config.mjs`:

```js
// other imports...
import { babel } from '@rollup/plugin-babel';

export default defineConfig({
  plugins: [
    // other plugins...
    babel({ babelHelpers: 'runtime', extensions }),
  ],
});
```

The plugin `babel` from [`@rollup/plugin-babel`](https://www.npmjs.com/package/@rollup/plugin-babel) is the piece that considers the Babel configuration file. Vite plugins are based on Rollup's plugin interface with a few extra Vite-specific options. Therefore, Rollup plugins are compatible with Vite and can be used as is in Vite's configuration. This is the reason why if you write a Vite plugin that uses only features inherited from Rollup, then [the convention is to name it a Rollup plugin](https://vite.dev/guide/api-plugin.html#conventions).

## Ember Inspector structure

- [Ember Inspector](https://github.com/emberjs/ember-inspector) is an Ember app that shows in an iFrame and gets information from the main Ember app displayed on the page.
- To make communication possible, it injects a debug module on the page. This module is responsible for accessing and passing the required data to the inspector.

This approach doesn't work with Vite because it relies on AMD modules and globals. We must find a new way to let the inspector communicate with an Embroider+Vite app. This work counts several steps that we touched upon this week:

- Understand how the information is communicated for a Classic Ember app
- Define the new protocol to communicate information from an Embroider+Vite app
- Implement this protocol

<br />
<br />

_Ember Inspector is an important subject for the Ember Initiative. It will be our main focus starting next week. The current goal with the budget we have is to write the RFC. I'll also keep working in parallel on a few open issues we have on ember-vite-codemod. For the Ember Initiative to continue, we need your support 🐹❤️ [Get in touch with Mainmatter](https://mainmatter.com/contact/)._

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md), 
[Week 7](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-7.md),
[Week 9](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-9.md)

