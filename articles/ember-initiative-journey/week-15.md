# The Ember Initiative Journey 🐹❤️

_Week 15 - Reworking the plan_

_#web #emberjs #ember_inspector #rfc #embroider_compat_

The main event of the week is that the RFC we wrote for Ember Inspector won't be accepted as is. The compatibility part of it is roughly ok, but what the Ember Inspector should be in the future should be redesigned more drastically. In other words, we designed a solution based on how to reuse existing pieces, but the Core Team is unhappy with the existing pieces in the first place.

## Adjusting the strategy

Getting the RFC rejected is not necessarily bad news. It doesn't change our work really: We still need to bring Vite support to Ember apps from 3.28 to latest, which don't and never will have the new API that allows Ember to expose ESM module to the Inspector. So we have a compatibility piece to implement, and this piece is time sensitive since developers who moved to Vite are already stuck with a non-functional inspector.

The only part of the plan that changes for us is the post-RFC part: We wanted to get the RFC accepted, then implement it. Instead, we will rework the RFC and leave it in a state that explains the direction to take in the future, but we won't do the implementation. It doesn't enter the current budget, and the priority is lower than the compatibility piece anyway.

The RFC has been moved back to draft, and the current content already redefines the problem: https://github.com/emberjs/rfcs/pull/1119

## Starting the compat API

This week, I started the implementation of the support script in `@embroider/compat.inspector-support`. It's a TypeScript package that compiles files based on a config. However, it doesn't work well with the static script we want to provide. Interestingly, a working solution was to make the script an `mts` that compiles to `mjs` so we have the ESM shape in output.

I am afraid this is the only tech tip I have to share this week. Now, the rest of the work is to get a new prototype working with this script to finalize the PR with proper testing instructions. This doesn't go as smoothly as I was hoping for, but I am confident I will reach that goal soon enough.

<br />
<br />

_I am now following 3 paths in the Ember Initiative journey: the "compat" inspector support for Vite, rethinking the perfect API for the RFC, and preparing the EmberFest that will happen in September._

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md),
[Week 14](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-14.md)
