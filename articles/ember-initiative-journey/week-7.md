# The Ember Initiative Journey 🐹❤️

_Week 7 - the short week_

_#web #emberjs #embertestselectors #babel #babelconfig_

This week has been very short for the Ember Initiative since we had a team event at Mainmatter. I tried to move on with my tasks, but I couldn't properly finish anything.

## ember-test-selectors for Vite

[ember-test-selectors](https://github.com/mainmatter/ember-test-selectors) is an addon managed by Mainmatter that belongs to the top 100 addons. Since it's a popular addon, we need to move it to V2 world like we've already did for `ember-simple-auth`, `ember-cookies` or `ember-promise-modals`.

### The classic addon works for Vite...

ember-test-selectors is this kind of classic addon that does things at build time and, therefore, is not a great candidate for a migration to v2 "as is".

ember-test-selectors relies on a boolean option that means "strip" or "don't strip" the `data-test-*` attributes from the templates. When the option is `true`, the addon builds a [Babel plugin](https://babeljs.io/docs/plugins/#plugin-development) and adds it to the list of processes to execute. There are two different Babel plugins: the "main" one strips the `data-test-*` attributes in your templates, and the second one also strips `data-test-*` properties from JS objects.

`@embroider/compat` is the part of Embroider in charge of making classic addons work in Vite apps whenever it's possible. Among other things, it generates a list of "Babel compat" plugins out of all the plugins added by classic addons, and these "Babel compat" plugins are added in the `babel.config.mjs` of the Vite app through `babelCompatSupport` and `templateCompatSupport` functions. `@embroider/compat` is able to rewrite the behavior of ember-test-selectors correctly. The Babel plugins built by the addon are added to the Babel config of the Vite app using the "Babel compat" feature. In other words, using the classic addon ember-test-selectors doesn't block your migration to Vite. 

However, if you start from a Vite app and want performances to benefit from `@embroider/compat` not running, then ember-test-selectors should provide a solution.

### ...but we need a solution for users who don't build the compat addons

V2 world is different from classic world in two aspects: v2 addons don't impact the build pipeline; the app is responsible for the configuration (e.g. Babel configuration). Before, we had a classic addon adding a Babel plugin to the pipeline; now, all we want is that very same Babel pipeline added to the `babel.config.cjs` directly. Since the app is responsible for the configuration, the Babel plugin doesn't have to care about the external context (is a production or a dev build, do we want to force the stripping, etc...) Instead, we document how developers can configure Babel to have the default behavior (strip in production) and let them free to change this config if they have very specific needs.

To sum it up, the plan is the following:

- Refactor ember-test-selectors structure to a monorepo that separates the classic addons from tests
- Separate the Babel plugins (strip-test-selectors and strip-data-test-properties) from the classic addon and get the classic addon install them.
- Create a vite-app in the tests folder of the monorepo and install the package strip-test-selectors to run tests on the Babel configuration.

## About testing

One thing tricky to manage with ember-test-selectors is testing. Since stripping `data-test-*` only happens in production, your tests would fail if you run them in the browser. In the classic version of ember-test-selectors, the environment variable `STRIP_TEST_SELECTORS` was used to change the behavior of the addon: the stripping happened even in a test build if the variable was `true`, so depending on its value, the correct set of test (it strips or it doesn't strip) runs.

It's absolutely possible and legit to use such an environment variable in the Babel config of the vite-app used by the monorepo for testing. After all, we want to test the behavior of the strip-test-selectors plugin, not the behavior of the Babel config. But since we want to explain to developers how they can configure the "strip only in production", we could also consider it legit to base the test on this specific scenario, production vs development. Testing the development mode in CI is a bit more complicated, though, because we need to start a Vite dev server.

Testing in development mode should probably be considered an enhancement, separated from introducing the strip-test-selectors Babel plugin.

<br />
<br />

_Embroider 4 was finally released this week, we are on good rails to make Vite the default for new Ember apps. This is why the work on the top 100 addons is so important, since we don't want new apps to rely on the installation of classic addons. This weekly log was written from the train, I did my best ;)_

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md), 
[Week 5](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-6.md)
