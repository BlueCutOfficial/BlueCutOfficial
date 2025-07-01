# The Ember Initiative Journey 🐹❤️

_Week 13 - Ember Inspector blog post & manual testing tips_

_#web #emberjs #blog_post #ember_inspector #vite #npx #pnpm_dlx_

I promised it last week, here it is! I wrote the blog post [The road to Vite support for the Ember Inspector](https://mainmatter.com/blog/2025/06/20/ember-inspector-vite/). It will explain everything my team is doing with the Ember Inspector in the big lines: what's the problem, what's the plan, where we are... Everything I mentioned in the past weeks, but after taking a step back now that we are making proper progress.

### The Inspector "snapshots"

The Ember Inspector has an interesting concept of "snapshots". In very simple words, you can freeze a version of the Inspector and say: this frozen version should be downloaded if the Ember app running on the page is in that given version range. This way, you can stop supporting old Ember versions, and if a developer wants to inspect a super old Ember app, it will be inspected with an old but functional version of the Inspector.

That said, the current Ember Inspector supports Ember app back to 3.16, which is already quite old. At the moment, we can't do any substantial change in the inspector that would break 3.16 tests.

When a specific CI scenario fails for a version, combining `ember-try` and running tests in the browser is a good way to start a debugging session. But sometimes, tests are not your best entry point when you just want to try out a specific thing you have in mind, and is not connected to your current test cases. 

### `npx` and `pnpm dlx`: run commands from remote npm packages

Did you know that you don't need `ember` installed globally on your machine to run `ember` commands? [npx](https://docs.npmjs.com/cli/v8/commands/npx) and [pnpm dlx](https://pnpm.io/fr/cli/dlx) offer ways to execute commands from remote npm packages. Since the package syntax includes the version (`my-package@x.x.x`), you can execute CLI commands from any old version you choose.

The command `ember` you get when you install Ember CLI globally on your machine comes from ember-cli npm package. So let's say you want to test a specific feature like "Does ember-wormhole < 0.5.0 work in a 3.16 app?" (no, it doesn't). You can generate a 3.16 ember app with:

```
pnpm dlx ember-cli@3.16 new my-old-3-16-app
```

Personally, I have a folder on my computer that contains various versions of Ember apps from 3.16 to 6.4, using Broccoli, Embroider+Webpack, or Embroider+Vite build pipeline. I add this folder to almost all my VS Code workspaces. For instance, in my Ember Inspector workspace, I have four folders: the ember-inspector fork from Mainmatter, the ember.js fork that Chris Manson created for our proof of concept (see [blog post](https://mainmatter.com/blog/2025/06/20/ember-inspector-vite/)), the embroider repo that I used to draft the quick-fix plugin (still in the [blog post](https://mainmatter.com/blog/2025/06/20/ember-inspector-vite/)), and _that_ folder I called "Ember app fixtures" that contains all the Ember apps I regularly use for diverse manual testing.

### A word about `ember-wormhole`

[ember-wormhole](https://github.com/yapplabs/ember-wormhole) is an old addon that is used to render a part of your template in a given "distant" DOM element instead of right in place. It was developed before Ember provided the built-in `in-element` and still has a few more features. Because of the type of feature this is, ember-wormhole has dedicated support in the Ember Inspector, and it's part of the things that require a bit of refactoring to prepare the ground for Vite. This is one more challenge we raised as we are working on the Ember Inspector code: design the best strategy regarding ember-wormhole support.

<br />
<br />

_I am happy about our current progress on the Ember Inspector. Writing the blog post was a good exercise to take a step back and realise what we have already achieved regarding the plan. I am confident that it communicates the project's complexity well enough and explains why so many weeks are necessary to deliver a stable solution._

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md),
[Break & Weeks 11-12](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/break-weeks-11-12.md),
[Week-14](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-14.md)
