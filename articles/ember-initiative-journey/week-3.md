# The Ember Initiative Journey 🐹❤️

_Week 3 - supporting @embroider/webpack_

_#web #emberjs #codemod #embroider #vite #vitest #testem_

At the end of this third week, ember-vite-codemod brings Vite to your Ember app formerly building with `@embroider/webpack`, and this case is tested by the CI, which is the important part.

## From `@embroider/webpack`to `@embroider/vite`: easy peasy?

At the time of writing, [Embroider's README](https://github.com/embroider-build/embroider?tab=readme-ov-file#how-to-try-it) describes how to start building a classic app with `@embroider/webpack`; and it's quite straightforward, the only file that changes is `ember-cli-build.js`.

This is very good news for our codemod because `ember-cli-build.js` turns out to be the only file that requires adjustments to support a migration from `@embroider/webpack`. In other words, the hard part is already done, once the `ember-cli-build.js` can be handled as "I start from classic" and "I start from Embroider+Webpack", the rest of the codemod works exactly the same as before.

To manage this, I introduced a new option: `--embroider-webpack`. It helps the codemod understand what the initial situation is rather than trying to detect it somehow. The PR also [adapts the documentation](https://github.com/mainmatter/ember-vite-codemod?tab=readme-ov-file#from-embroiderwebpack) to the changes.

Easy peasy? Not quite. If I spent half a day on the implementation itself, tests have been more challenging.

## Testception

### Port 7357 already in use:need-a-sad-hamster-emoji:

The most interesting challenge from this week has been to build a good mental image of ember-vite-codemod's tests. The error I had to fight was "port already in use :7357". This error means that I am instantiating a server with a port that is already used by another running server. But why does it happen?

If you're familiar with the Ember ecosystem, you may have recognized that port number: it's [Testem](https://github.com/testem/testem)'s default port! But why would I have different Testem servers listening at the same time? It's basically a concurrency story, but getting it clear requires having a good representation of the tests' execution.

### What the tests do

We have three tests: one for classic Ember latest, one for classic Ember 5.12, and one for Embroider+Webpack Ember latest. These tests do exactly the same thing for each version. In the big lines:

- Generate an Ember app with `ember new`
- Create a simple acceptance test that visits the home page
- Build the app the old way (ember-cli + Broccoli)
- Run the tests (`ember test`) to make sure the acceptance test was passing in the first place
- **Run the codemod**
- Rebuild the app (it now builds with Vite)
- Run the tests once more to make sure they pass with Vite _build mode_
- Start a Vite dev server
- Run the tests again with Testem to check they pass with Vite _dev mode_

The point to pay attention to is that we have a test, and part of its instructions is to run an app's tests. Tests in tests. Testception.

`ember-vite-codemod`'s tests run with [Vitest](https://vitest.dev/guide/), so imagine three boxes: each box represents a test run by Vitest, "classic latest", "classic 5.12", "Embroider+Webpack latest". When tests are in the same files, they execute sequentially by default. But when tests are in different files, they execute in parallel by default. At the start, my new "Embroider+Webpack latest" test was executed in a separate file, whereas both classics were in the same file.

Now, in each box, imagine three other boxes of tests executing sequentially: first "legacy app", then "Vite app in build mode", then "Vite app in dev mode"; and these tests are Ember tests, which means they rely on Testem.

To sum it up, I have two Vitest test files that execute concurrently, and both tests they run try to instantiate a Testem server. The faster one does it; the second triggers a "port 7357 already in use".

From that perspective, Vitest is smarter than Testem; it can find available ports to manage concurrency. Testem, on the other hand, sticks to its default port if you don't pass a different one explicitly. The next part of the story is slightly less interesting in my opinion. I tried to use `portfinder` to solve the problem, but by the time the first server had started, `portfinder` had already returned the same port number to the second one. Ultimately, I found a way to specify the ports myself with an incremental number.

### Concurrency: make it work

My final solution was to have all the tests in one file (abstraction after abstraction, one file was more elegant), and I ran all three tests concurrently using `it.concurrent` from Vitest API. Each test uses Testem with a different port specified explicitly by an incremental number.

Getting concurrency work in such a test suite is important because each test is quite heavy: it generates an Ember app, tweaks its dependencies, builds it, and runs the tests several times. When I execute the tests sequentially on my MacBook at this stage of the project, it takes about 1'30~2'00 minutes per test, 5 minutes for all three. When I use concurrency instead, 1 minute is already saved. Since we want to enable tests for many other Ember versions and ideally add more unit tests for the transform scripts, managing concurrency correctly on our CI is not an option.

<br />
<br />

_This has been a short week for me (only three working days), but I am very happy with the outcome: the codemod now supports migration from `@embroider/webpack`, and I now have a clear mental picture of what the CI does. Chris Manson is currently working on getting Vite work for Ember < 5.12 (this involves Embroider doing some patching on ember-source itself); it's only when he's done that it will make sense for our codemod to support these older versions. Meanwhile, though we could improve the codemod indefinitely, we must also deal with the rest of the tasks planned for the first quarter. I think it's time for me to tackle the [audit of the top 100% Ember addons](https://github.com/orgs/mainmatter/projects/14/views/3?pane=issue&itemId=95485013&issue=embroider-build|embroider|2288) to get a sense of where the community is on that field._

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md), 
[Week 2](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-2.md)
