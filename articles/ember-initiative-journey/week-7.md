# The Ember Initiative Journey 🐹❤️

_Week 7 - the short week_

_#web #emberjs #embertestselectors #embervitecodemode #buildmode_

This week has been very short for the Ember Initiative since we had a team event at Mainmatter. I tried to move on with my tasks, but I couldn't properly finish anything.

## ember-test-selectors for Vite: the new approach

[ember-test-selectors](https://github.com/mainmatter/ember-test-selectors) is this kind of classic addon that does things at build time and, therefore, is not a great candidate for a migration to v2 "as is". Let's sum up its behavior.

ember-test-selectors relies on a boolean option which means "strip" or "don't strip" the `data-test-*` attributes from my templates. 

//

## Vite mode and Ember mode

One thing a bit tricky to manage with ember-test-selectors is testing. Since stripping `data-test-*` only happens in production, your tests would fail if you run them in the browser. In the classic version of ember-test-selectors, the environment variable `STRIP_TEST_SELECTORS` was used to change the behavior of the addon: the stripping happened even in a test build if the variable was `true`, so depending on its value the correct set of test (it strips or it doesn't strip runs). 

//
