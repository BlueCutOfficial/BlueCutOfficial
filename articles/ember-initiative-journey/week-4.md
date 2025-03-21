# The Ember Initiative Journey 🐹❤️

_Week 4 - the start of the addon audit_

_#web #emberjs #emberobserver #publicapi #embercssmodules #emberscopedcss_

This has been a tough week, in the sense that I see a lot of work coming! As usual, I'll keep this weekly log short and focus only on a few noticeable points.

## The start of the addon audit

We released [ember-vite-codemod](https://github.com/mainmatter/ember-vite-codemod) to get classic Ember apps to build with Vite, and I wrote a [blog post](https://mainmatter.com/blog/2025/03/10/ember-vite-codemod/) about it on Mainmatter website. So far, so good. But will people be able to use the codemod without any trouble? A part of the answer depends on the addons they use. If they use a v1 addon (classic Ember addon) that is incompatible with Embroider+Vite requirements, at least part of the functionalities will break.

How to evaluate the risk of an app being blocked by an addon? We certainly can't control all the existing addons, but there's a valuable tool that can be used here: [Ember Obsever](https://emberobserver.com/). Ember Observer is a website that allows us to view and search all the existing Ember addons and sort them [by score](https://emberobserver.com/about).

What I am interested in is [the top 100](https://emberobserver.com/lists/top-addons). How is this list displayed? If I go to my browser's network tab, I can see the exact request to the public API: https://emberobserver.com/api/v2/addons?filter[top]=true&include=categories&page[limit]=100&sort=ranking.

I created a simple node script that performs the same request with `await fetch`, then I used the result with `npm view` (like it's done in the [codemod](https://github.com/mainmatter/ember-vite-codemod/blob/main/lib/tasks/ensure-v2-addons.js#L32)) to split the response between v1 addons and v2 addons.

The outcome is a list of 46 v1 addons in the top 100. With Chris' help, I sorted them into 3 categories:

1. The v1 addon should be compatible with Embroider+Vite
2. The addon functionalities are too tied to the classic world and this addon has no future in Embrodier+Vite
3. We are not sure about the compatibility, the community should help us test this addon and eventually convert it to v2. 

Here is the [work-in-progress table](https://github.com/embroider-build/embroider/issues/2288#issuecomment-2713639700). 

## A migration path for ember-css-modules

In our 3 categories of v1 addon, there's one we are especially interested in as part of ember-vite-codemod improvement: "2. The addon functionalities are too tied to the classic world and this addon has no future in Embrodier+Vite". If one of these addons is detected in the package, we should warn the user about it. We already do it for a few addons like `ember-fetch` and `ember-cli-mirage`, but now we have new candidates.

The problem is that before telling people to remove an addon from their dependencies, we need to provide an alternative. How to re-implement what the addon was doing a way that is compatible with Vite world? For now, this migration path doesn't exist for [ember-css-modules](https://github.com/salsify/ember-css-modules), which is one of our "to-remove" addons. Before allowing the codemod to detect it, we need to draw the migration path.

This is the next step of my work on the Ember Initiative. I started a repository to present a possible migration to [ember-scoped-css](https://github.com/soxhub/ember-scoped-css).

### The diff view once again

In the weekly log about the codemod, I explained how we used [Beyond Compare](https://www.scootersoftware.com/) to have a view of the differences between the classic app and Vite app. 

I decided to go with the same kind of "diff view approach" here: showing developers a before/after using the GitHub interface. Here is how I sructured the repository:

- I have an ember-css-module branch that contains a simple classic Ember app using ember-css-module
- Out of this branch, I created a second branch where I migrate this app to ember-scoped-css
- In the `main` branch, I only have a README that contains the URL to the diff. On GitHub, you can see the diff between two branches using the URL: `baseURL/Owner/Repository/compare/branch1..branch2`.

Now, the other big part of the job is to understand and explain the differences between both addons. I won't go into details in that weekly log because you'll be able to read everything when I communicate about the repository.

<br />
<br />

_It's nice to see how enthusiastic the community is about the Ember Initiative. We started to communicate about the codemod, and we already have PRs and issues opened. The hard part on the organizational side will be to prioritize these new issues compared to the work we have already planned. Supporting Vite in older Ember versions and providing migration paths for all addons that are not relevant in Vite world are the priorities we need to stay focused on._

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md), 
[Week 3](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-3.md)
[Week 5](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-5.md)
