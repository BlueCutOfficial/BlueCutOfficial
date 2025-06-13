# The Ember Initiative Journey 🐹❤️

_Break and come back_

_#web #emberjs #ember_inspector_

For budget reasons, the Ember Initiative stopped on April 25th. After a one-month break working on another project and enjoying vacation, the Ember Initiative started again on May 20th.

That said, May is a weird month for French people: We have a lot of public holidays, and unfortunately, I had to take a few additional days off for health reasons. To sum it up, I didn't work that much in May. Because of this, I spent all of my work time (a very short time) focusing on our current topic (the Ember Inspector) and didn't communicate. I prefer to forget that May 2025 ever existed in my professional life and consider that the Ember Initiative truly restarted the first week of June.

June has been a more regular month so far, so I should have restarted these weekly logs last week and talked to you about our progress on the Ember Inspector. I missed last week in the end, but I'll restart today.

## Last news about Ember Inspector

Getting the Ember Inspector to work with Ember+Vite apps is currently the primary focus of the Ember Initiative. Though the goal is very simple to state, how to reach it is another story and requires the Ember Inspector project to have its own micro-roadmap.

We are implementing the strategy I presented in Week 9, except that a few parts have been inverted and added. My goal today is to write about this in an actual Mainmatter blog post. It will give you a way better overview of the plan and where we are now.

What I can say now is that we've been making significant progress over the past two weeks:

- The inspector's test suite has been fixed: it continues to support back to 3.16, and 6+ versions are also green.
- The inspector script that runs on your page now builds with Rollup.
- We have started a refactoring work that will centralize how the inspector script imports Ember modules in one file, so the other part of the script can be agnostic of the build system used by the Ember app on the page.

<br />
<br />

The Ember Inspector has not been easy to approach. When we started to focus on it, I could only see a ball of knots with wires sticking out. After two full 4-day weeks, we're finally making significant progress. This project could still hide challenging surprises, though.

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md), 
[Week 9](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-9.md),
