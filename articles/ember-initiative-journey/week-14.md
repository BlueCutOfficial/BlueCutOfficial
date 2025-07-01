# The Ember Initiative Journey 🐹❤️

_Week 13 - Ember Inspector & preparing Ember Fest_

_#web #emberjs #ember_inspector #ember_fest #auto_reveal_

There was not much coding this week. The primary goal was to draft the first version of the RFC so that the core team could challenge it. And to draft the RFC, I had to investigate more about the relevance of what the inspector currently imports.

## Watching for rabbit holes

This week's investigations led me to a bug in the current Inspector: most services are marked as computed properties instead of proper services. This is because the way the inspector detects if an object is a service no longer fits the supported Ember versions. (A week later, this kind of problem will explain a downside in the approach we suggested for the new API.) The reason I found this bug is that the piece of code involved uses `instanceof Service`, where `Service` is imported from Ember.

Ember Inspector tasks are hard to estimate because this type of project is very "R&D like". To avoid consuming too much time, developers must constantly keep the main objective in mind and be very careful with the wires they decide to follow. For instance, my objective is to implement Vite support for the Inspector, preferably before Vite becomes the default when executing `ember new`. Does the bug I found relate to this objective? If I fix the bug, what are the chances that `instanceof Service` is still present in the fixed code? If chances are high that importing `Service` makes sense, then fixing this bug is not my priority because it doesn't change the API the Inspector needs to consume.

When you're working on a complex project with hard-to-scope tasks that can't be estimated, the primary goal is what you should refer to each time you need to choose a path. 

## auto-reveal

In parallel with the Inspector project, we must prepare the talk we will give at [EmberFest](https://emberfest.eu/) about the Ember Initiative. We will create the slides with [auto-reveal](https://github.com/mainmatter/auto-reveal).

It's a library owned by Mainmatter that brings a CLI at the top of [reveal.js](https://revealjs.com/) and automates things about theme building.

<br />
<br />

_The first version of the Inspector RFC has now been submitted, and since we managed to post it right before a Core Team meeting, we will get news next week. Meanwhile, we are continuing the refactorings on the Inspector side, and we are moving forward with the EmberFest talk._

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md),
[Week 13](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-13.md)
