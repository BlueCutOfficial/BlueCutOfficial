# The Ember Initiative Journey 🐹❤️

_Week 6 - starting the upgrade of ember-test-selectors_

_#web #emberjs #migrationStrategy #embercssmodules #emberscopedcss #monorepo #embertry_

This week has been a week of transition in my Ember Initiative journey. I am moving from one topic to another, which gives me a false feeling of incompletion that doesn't truly reflect how things have been moving. My 3-day week in a nutshell: I am done with the migration path from ember-css-modules to ember-scoped-css, I started to work moving ember-test-selectors to v2, and I handled a few issues on ember-vite-codemod.

### The migration path about ember-css-modules is out

I spent most of Week 5 working on the migration path to get rid of ember-css-modules; the blog post is out: [Get ready for Vite, migrate from ember-css-modules](https://mainmatter.com/blog/2025/03/28/migrate-from-ember-css-modules/). I am rather happy with its structure and the repository-approach I used, that could be a pattern to reuse in the future.

The whole point of this work was to provide developers with a way to get rid of ember-css-modules CSS file by CSS file. Splitting your work into multiple small PR is indeed a good practice to ease reviews and manage important migration confidently. Talking about that...

### The best way to turn a classic addon into a monorepo?

If you want to convert a classic v1 addon to v2, one first PR should be refactoring the repository to a monorepo that separates the classic addon and the dummy app into two separate packages. You don't change how things work; you only change the repository's structure.

Explaining how to do this is the purpose of [Guide: Porting an Addon to V2, Part 1: Separate Addon from Dummy App](https://github.com/embroider-build/embroider/blob/main/docs/porting-addons-to-v2.md#part-1-separate-addon-from-dummy-app). I used this guide myself in the past (to migrate ember-promise-modals to v2) and I even contributed to clarify a few things I had problems with. And when I used this guide again for ember-test-selectors, which has a slightly more complex hierarchy, I realized...

The guide Porting an Addon to V2 didn't provide the easiest way for me to proceed, and it was very interesting to come to that conclusion.

The best way for me to proceed is first to create a single-package monorepo: I make the monorepo structure with only my v1 addon package in the workspace. That step allows me to start with a super clean root: brand new private `package.json`, no confusing ESlint config, `scripts` commands that target the addon package, etc... And once I have this working, I can start to create new packages from scratch (test-app, node-tests...) and copy or move into them the content of the v1 addon package. It allows a more step-by-step approach where I can try the lint and test commands for each new package to ensure I don't forget anything.

### A tiny detail about ember-try

When I created the monorepo for ember-test-selectors and pushed my work on GitHub, I had all the Ember versions matrix failing because of "ember-try config not found". At first, I thought I had made an error in the CI workflow: Maybe the working directory wasn't correctly set? But I couldn't see the problem; the workflow seemed correct.

I eventually figured out that the option `useVersionCompatibility` invalidated the ember-try config. This option should be set only when ember-try is used to test an addon against multiple Ember versions:

```
/*
  If set to true, the `versionCompatibility` key under `ember-addon` in `package.json` will be used to
  automatically generate scenarios that will deep merge with any in this configuration file.
*/
useVersionCompatibility: true,
```

Since I restructured the repo to have a simple Ember app `test-app` completely separated from the classic addon, I should have removed `useVersionCompatibility`. But rather than telling me about an invalid config, the CI was telling me "ember-try config not found".


<br />
<br />

_We have achieved so many things in 6 weeks, and there are still so many things to do. I am rather happy with my own cruising speed so far: I manage to handle the issues people left on ember-vite-codemod and still spend most of my time moving on the main goals. I wish I could hope that next week would be the week I am done with ember-test-selectors update, but I won't be that bold since it will be a very short week (we have a team event at Mainmatter). No doubt I'll be able to work on a few new improvements for ember-vite-codemod. I can't say it enough: the Ember Initiative is very important for the whole Ember community, our team is achieving amazing things for the framework, and we need your support to continue. Please [get in touch with Mainmatter](https://mainmatter.com/ember-initiative/)._

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md), 
[Week 5](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-5.md),
[Week 7](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-7.md)


