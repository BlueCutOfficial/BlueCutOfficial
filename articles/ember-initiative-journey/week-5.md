# The Ember Initiative Journey 🐹❤️

_Week 5 - between codemod improvements and migration paths_

_#web #emberjs #backwardCompatibility #embercssmodules #emberscopedcss #vite #vitest #snapshotTesting_

This week has been very productive. We have Vite support for Ember 3.28, the migration path from ember-css-modules to ember-scoped-css is now clear, and we fixed a couple of issues in [ember-vite-codemod](https://github.com/mainmatter/ember-vite-codemod).

The Ember Initiative started a month ago, and we have already achieved a few critical goals. If you want us to continue, please support the initiative. It aims to secure the Ember ecosystem in the long run with continuous development and improvements. [Get in touch with Mainmatter](https://mainmatter.com/contact/) to support and decide on our team's priorities.

## Documenting: a good way to raise issues

Something interesting about documenting how to do something with a minimalist example is that you must be able to build this example yourself. Since we want to tell developers to stop using ember-css-modules because it's incompatible with Vite, we also need to tell them how to migrate to another solution and, therefore, perform that migration ourselves to make sure the path is valid.

Chris Manson suggested that our recommendation should be to replace ember-css-modules with ember-scoped-css. He suggested that because he knows for a fact this solution enables a file-by-file migration, which is an absolute requirement to migrate a big codebase alongside production development. He knows that because he has already experimented with this solution in a past project to which Mainmatter contributed. But interestingly, the layers of complexity in this past project resulted in not hitting issues that my way-more-simple example hits.

When I implemented a "guide repository" to explain to people how to migrate from one addon to another, I realized that both addons have their own oddities, and figuring out who was doing what wrong was some tricky exercise. In the end, a pair session with Chris led to [a new option in ember-scoped-css](https://github.com/soxhub/ember-scoped-css/pull/285) to improve the way it interoperates with other addons like ember-css-modules. Only then could I finish the migration guide. 

 ## Snapshot testing in Vitest: a new definition of "easy"

I haven't used snapshot testing that much in my career, so I don't have an accurate overview of the available tooling. What I can say for sure is that Vitest's simplicity is just outstanding. 

The library includes an out-of-the-box snapshot API. This API provides a very interesting feature, [inline snapshots](https://vitest.dev/guide/snapshot.html#inline-snapshots), which generates the snapshot result directly in the test as a string. This is a very nice-to-read solution for small objects, and it works exactly as the classic snapshot generated in a separate file.

Additionally, the CLI allows you to update the snapshot by pressing `u` during the test watch — because Vitest watches your tests — which is awesomely handy and easy to use.

<br />
<br />

_At the time of writing, the latest Ember is 6.x. Ember 3.28 is three major versions prior, it was released several years ago, and it now supports Vite. This is what the Ember community means by "support". It's a very important achievement, and I hope it will encourage developers working with old versions to pave their way to Vite and adopt all the modern practices step by step._

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md), 
[Week 4](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-4.md)
 
