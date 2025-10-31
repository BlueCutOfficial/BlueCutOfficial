# The Ember Initiative Journey 🐹❤️

Week 19 - The road to v2 for ember-scroll-modifiers

_#web #emberjs #open_source #ember_scroll_modifiers #addon_v2 #migration_steps #guides_

This week, I had two workdays allocated to the Initiative. I am thrilled to say that they've been well used, but I wish I could have more time to tackle a bigger scope. Fortunately, there is a type of task that perfectly fits ~2 or ~3 days, and this is the conversion of a community addon to v2 format.

## Tips and learnings from _ember-scroll-modifiers_

### The "easier" order

First of all, when you want to migrate a classic addon to v2, I strongly encourage you to manage the migration with several PRs. You may feel like you're wasting time, but I firmly believe that the confidence you and your reviewers will have in the migration is worth it. Since _ember-scroll-modifiers_ has a pretty standard shape and provides modifiers, the PRs split I did is my personal recommendation (⚠️ commits are important): 

- https://github.com/elwayman02/ember-scroll-modifiers/pull/1268 - Use pnpm package manager
- https://github.com/elwayman02/ember-scroll-modifiers/pull/1273 - Make sure the CI is in a decent state
- https://github.com/elwayman02/ember-scroll-modifiers/pull/1274 - Separate the addon and demo-app into two different packages
- https://github.com/elwayman02/ember-scroll-modifiers/pull/1275 - (Optional) Untangle the demo (docs) and the tests
- https://github.com/elwayman02/ember-scroll-modifiers/pull/1276 - Convert the addon package to V2

💡 Note that "Untangle the demo and the tests" is not necessarily critical if your tests are green in the first place. On _ember-scroll-modifiers_, this step was important because test results were misleading: they were failing because of the documentation tool and not because of the addon itself.

### Be careful with the porting guide

If you want to convert an addon to v2, you may naturally have a look at the ["Guide: Porting an Addon to V2"](https://github.com/embroider-build/embroider/blob/main/docs/porting-addons-to-v2.md).

I might have already said in a former weekly log that the method it presents is slightly different from mine: it gives a way to separate the addon and test-app in a single move, and I think it's way more clear to move the entire structure in a package first, like I did [in this commit](https://github.com/elwayman02/ember-scroll-modifiers/pull/1274/commits/214583c7f1a2bc033f1a571d5b7a834345d9a1c1), and move the test-app next, in a separate commit. But that's a personal preference, and that's not what I would like to warn you about here.

The main thing to note is that, at the time of writing, this porting guide is not up to date with the latest blueprint that generates a fresh V2 addon. Some dependencies have changed, and the monorepo structure has been abandoned. So, should you follow the porting guide? Or should you [create a fresh addon](https://github.com/ember-cli/ember-addon-blueprint) somewhere on your computer to study its structure and do the same?

```
pnpm dlx ember-cli@latest addon my-addon -b @ember/addon-blueprint --pnpm
```

For _ember-scroll-modifiers_... I made a mix of both approaches 🙈 (Yes, you can do that to 😬)

I suggested Jordan Hawker (the author) to keep the monorepo approach for a reason: the demo-app is based on _empress/field-guide_, which is incompatible with Vite at the moment. Therefore, the demo-app cannot be easily moved to Vite (upgrading _field-guide_ or rewriting the docs with a different solution are both considered "not easy" and certainly not doable with my 2-day budget). And the latest addon blueprint structure removes the monorepo in favor of a... global Vite setup, so going this way was potentially problematic. 

I followed the monorepo approach outlined in the porting guide, while also making the addon package more closely align with what the new addon blueprint provides (for instance, it uses the Babel configs of the blueprint instead of the legacy ones in the porting guides, etc). The main idea is that every time the porting guide said: install this, or use that file as an example, I rather had a look at what the blueprint does now.

<br />
<br />

_I am afraid this is, once again, my last weekly log for a while. Alas, I won't have any day allocated to the Ember Initiative for a while. I am quite satisfied with what I could do, though. When I was notified that I had only 2 days left, I was able to pick something that I thought would fit, and I would say I won my bet: the PRs are not all merged just yet, but they are green, described, and all ready._

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md), 
[Week 18](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-18.md)







 
