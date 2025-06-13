# The Ember Initiative Journey 🐹❤️

_Week 10 - Ember Inspector feat. Embroider_

_#web #emberjs #ember_inspector #vite #embroider #addons #blog_post_

I am posting this summary a few days late since I couldn't work on it last Friday, but here it is. Unfortunately, it might be my last Ember Initiative weekly update for a while, unless the Initiative receives more support. But let's start with the good news and return to this later.

## Ember Inspector

### Running the proof of concept

My primary focus this week was to get the Ember Inspector working for a Vite app — in other words, getting Chris' proof of concept to run on my side.

> You must have both of [Chris'] branches (the ember.js side and the ember-inspector side) running together. In other words, you need to [pnpm link](https://pnpm.io/cli/link) the `mansona/ember.js` branch to some Ember app you want to inspect, serve that Ember app, run the `mansona/ember-inspector` branch locally, and execute the script to load that local inspector in the app you are serving.

Using a local version of ember-source is not trivial; it requires building `ember.js`. A section of the [contributing guide](https://github.com/emberjs/ember.js/blob/main/CONTRIBUTING.md#building-emberjs) is dedicated to this. Note that by `pnpm link ../../path/to/ember-source`, they mean the path to your local `ember.js` repository containing the `package.json` and the `dist` folder you've built. I personally had to fight with my local link to `ember.js`: I was blocked by errors unrelated to the inspector, and to move forward, I had to comment out the component invocations in my Vite app template so they don't trigger issues. But that was it to have the proof of concept running 🎉

Using this base, I was able to start digging into the inspector code and familiarize myself with the first issues we should fix. 💡 The ember-inspector repository contains an `ember_debug` folder, which builds to the script that will be injected into the main page to create the bridge between the inspector and the app. One silly point I struggled with is applying the local changes I make to the `ember_debug` folder. I had to `pnpm build` the folder itself rather than run the build command from the root. Only then are my changes applied when using `pnpm serve:bookmarklet` to load the inspector locally.

### The draft on Embroider

The week's outcome is a [PR on the Embroider repository](https://github.com/embroider-build/embroider/pull/2455) that creates the same object, `emberInspectorLoader`, as Chris created on the ember.js side in the proof of concept. The approach was not obvious, though, because there are several ways to do it.

- **A regular virtual file?** Embroider includes a pattern to create virtual files like `vendor.js` or `test-support.css`, which are emitted as actual files in the Rollup build. I am pretty familiar with this part of Embroider since I wrote a few of them during the Embroider Initiative in 2024. However, there was something odd about using this core system for a classic feature support, especially with the `@ember` namespace that is not a "virtual" thing; we ultimately want `@ember/debug/inspector-support` to be provided by `ember.js`. So we decided to forget about this approach.

- **ember-source compat adapter** Embroider "compat" is the part of Embroider that manages compatibility with classic features. It includes a concept of compat adapter that allows patching addons. That system can be used to create a new file in the versions of ember-source that support Vite, so people using Vite from 3.28 to latest have this additional script that provides `emberInspectorLoader`. Aside from the relative simplicity, another advantage of this approach is that we can tweak the script depending on the Ember version. For instance, Ember < 4.8 didn't have an export for `@ember/enumerable/mutable`, so if the user is between 3.28 (included) and 4.8 (excluded) there's an object used by the inspector we need to get from somewhere else. The problem, though, is that compat adapters patch only v1 addons, and starting 6.1, ember-source has become v2, so compat adapters don't cover everything we need.

- **a dedicated Vite plugin** The last approach I tried is a dedicated Vite plugin, inspectorSupport(). It's an extra-simple version of regular virtual files. If `@ember/debug/inspector-support` was never resolved before and ends up passing into the `resolveId()` function of the plugin, then I resolved to a specific identifier, and the `loads()` function for this identifier returns the script we need. Using this approach in combination with compat adapter for 3.28 - > 4.8 range allows to get `@ember/debug/inspector-support` resolved for each version.

## The addons audit blog post

During [Week 4](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-4.md), I described how I used Ember Observer's API to get a picture of the status of the top 100 Ember addons.

This week, this audit was concluded by a blog post: [Getting ready for Vite! The status of the top 100 Ember addons](https://mainmatter.com/blog/2025/04/25/ember-addons-audit/). The blog post is not only about the result of the audit, but also about how it impacted our Ember Initiative roadmap. For instance, thanks to this audit, we saw how important `ember-css-modules` and `ember-test-selectors` are for the community, which is why I worked on these two addons (mainly in Week 5 and Week 7).

Additionally, the blog post includes sections clarifying the situation around Webpack and FastBoot, so if you're interested, have a look.

## We need support

The first three months are coming to an end, and unfortunately, we have to slow down the Ember Initiative. We're actively working on getting new sponsors on board to fund development for the next 3 months. You can help make this happen:

- Share Mainmatter's [call-for-sponsors](https://fosstodon.org/@mainmatter/114392807615590857) posts on social media.

- Talk about the Ember Initiative around you and in your company.
  
- Share your experience if our work helped you migrate your Ember app to Vite.
  
<br />
<br />

We have achieved so many things in 10 weeks of work. I am very enthusiastic about the impact it has on the Ember community, and I sincerely hope the Ember Initiative can continue with more support.

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md), 
[Week 9](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-9.md),
[Break & Weeks 11-12](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/break-weeks-11-12.md)
