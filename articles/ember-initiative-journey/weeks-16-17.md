# The Ember Initiative Journey 🐹❤️

_Weeks 16 & 17 - Moving forward on the new plan_

_#web #emberjs #ember_inspector #virtual_files #embroider_compat_

## New backers for the Ember Initiative

We've got new sponsorships for the Ember Initiative! 🎉 This means we have enough budget to work until September. This should be enough time to finish the Inspector's compatibility piece and unblock Vite users. If possible, we will have started the next topic by this time.

## Continuing Vite support for the Ember Inspector

The Inspector's compatibility piece gives the impression of moving forward slowly. It's not that Chris and I are slow; it's just that the project is stupidly hard.

On the inspector side, while Chris is still working on the new Rollup build to use ember_debug as ESM module, I have finally achieved 100% the centralization of everything that calls Ember modules in ember_debug code. The end of the job is materialized by [the removal of `export default Ember;`](https://github.com/emberjs/ember-inspector/pull/2669/files#diff-b563250ea6955e99d6516e76c1e20fa93b64802e1e0158ff6f4fcd83cbb1c6d1L193) from the utils responsible for accessing the Ember modules.

On the Embroider side of the thing, our POC reached a shape where we could present it to Ed for more practical feedback. The approach is accepted in the big lines, but there are two main tracks that can be followed for improvement:

- Continuing with the virtual files approach that I started.
- Trying to simplify things by making `@embroider/compat` a V2 addon and moving the virtual files as real files in `@embroider/compat`.

Both approaches have their own difficult details to handle, and I need more time to see the light at the end of the tunnel. Whatever the solution, we need to ease the maintenance by having one file per set of re-exports for each Ember version range (e.g. path for Enumerable mutable changed in 4.8), which creates a virtual file importing virtual file situation for the first approach. However, the second approach has also more weird context issues to solve.

## A coming topic about ember-exam?

Several people from different companies started to raise issues about using ember-exam in Vite. We didn't pay a specific attention to ember-exam because it has embroider optimized tests and a section of the README.md is literally called "How to use with Vite", it sounded promising enough to suppose the job was done. But apparently, there's something that is blocking people, and since the addon is ranked 33 in the top 100 addons at the time of writing, we should have a look into it if it's not fixed soon.

<br />
<br />

_The pace of the Ember Inspector has been a bit frustrating for me these past two weeks, but things keep moving, we are closer and closer to bring a solution to the community. The EmberFest in September will be an occasion to summarize the progress and find new sponsors so we can continue improving the framework for everyone._

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md),
[Week 15](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-15.md)
[Big Break](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/big-break.md)
