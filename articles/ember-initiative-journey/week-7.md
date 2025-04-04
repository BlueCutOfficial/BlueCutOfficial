# The Ember Initiative Journey 🐹❤️

_Week 7 - the short week_

_#web #emberjs #embertestselectors #embervitecodemode #buildmode_

This week has been very short for the Ember Initiative since we had a team event at Mainmatter. I tried to move on with my tasks, but I couldn't properly finish anything.

## ember-test-selectors for Vite

[ember-test-selectors](https://github.com/mainmatter/ember-test-selectors) is an addon manage by Mainmatter that belongs to the top 100 addons. Since it's a popular addon, we need to move it to V2 world like we've already did for `ember-simple-auth`, `ember-cookies` or `ember-promise-modals`.

### The classic addon works for Vite...

ember-test-selectors is this kind of classic addon that does things at build time and, therefore, is not a great candidate for a migration to v2 "as is". Let's sum up its behavior.

ember-test-selectors relies on a boolean option that means "strip" or "don't strip" the `data-test-*` attributes from my templates. When the option is `true`, the addon builds a [Babel plugin](https://babeljs.io/docs/plugins/#plugin-development) and adds it to the list of processes to execute. There are 2 different Babel plugins: the "main" one strip the `data-test-*` attributes in your templates, and a second one also strips `data-test-*` properties from JS objects.

`@embroider/compat` is the part of Embroider in charge of making classic addons work in Vite apps whenever it's possible. Among other things, it generates a list of "Babel compat" plugins out of all the plugins added by claissic addons, and these "Babel compat" plugins are added in the `babel.config.mjs` of the Vite app through `babelCompatSupport` and `templateCompatSupport` functions. `@embroider/compat` is able to rewrite correctly the behavior of ember-test-selectors. The Babel plugins built by the addon are added to the Babel config of the Vite app using the "Babel compat" feature.

### ...but we need a solution for users who don't build the compat addons

## Vite mode and Ember mode

One thing a bit tricky to manage with ember-test-selectors is testing. Since stripping `data-test-*` only happens in production, your tests would fail if you run them in the browser. In the classic version of ember-test-selectors, the environment variable `STRIP_TEST_SELECTORS` was used to change the behavior of the addon: the stripping happened even in a test build if the variable was `true`, so depending on its value the correct set of test (it strips or it doesn't strip runs). 

//
