# The Ember Initiative Journey 🐹❤️

Week 18 - Concatenating small things

_#web #emberjs #open_source #github #help_wanted #good_first_issue #fork #contributing #ember_scroll_modifiers_

The Ember Initiative needs more members so we can spend more time on it 🙏 Since my re-assignment, I could spend a bit more than 2 days working on the Initiative, and this time allowed me to do a few first things for the community. But to organize and tackle important topics like the new Route manager API, we need to invest a time that we don't have just yet. Mainmatter new plans make it easier for small companies to get onboard (I will post the extract of our talk about this when available).

## Open source tips for beginners

The Ember Initiative is mainly about open source things, but I feel like I didn't talk about the basics of open source development that much. Since I made my first contribution on `ember-scroll-modifiers` this week, now is a good time to get back to this.

### Want help or want to help: common labels

If you are interested in open source but you are new at it, one interesting thing to know is the "universal" conventions on GitHub. On GitHub, you can assign labels to Pull Request and Issues. When you create a new project, a few labels are already available by default, and two of them are very important to communicate with other developers: "help wanted" and "good first issue". Their meaning is quite explicit, but let's still develop:

- "help wanted": the maintainer of a repository should use this label when solving an issue or terminating a pull request requires time and resources they haven't. It's a literal call to help, but the complexity of the PR depends on the context.

- "good first issue": the maintainer should use this label on issues that they evaluate easy to do. It is something they could do themselves, but if they don't have time or have other priorities, they should to let this issue to anyone that would like to contribute without having a lot of knowledge on the repository yet.

### How to contribute: the actual basics

A long time ago, I was a developer who never contributed to an open source repository. When the time finally came, my innocent first action was to clone the repository, write my changes, and push a branch. But I wasn't allowed to push that branch... That was a bit problematic. How do you even contribute to a repository that doesn't belong to you? If you are a repository maintainer, I can only encourage you to explain the fork system, or point to resources that explain it.

As a contributor, in general, you are not allowed to push branches on someone else repository, unless you have been assigned as an official contributor. The standard way to proceed is to create your own fork of the repository. GitHub lets you do this very easily with the Fork button when you visit a repository. For instance, to contribute to `ember-scroll-modifiers` which belongs to `@elwayman02`, I created: https://github.com/BlueCutOfficial/ember-scroll-modifiers.

The PRs that are opened in `BlueCutOfficial/ember-scroll-modifiers` are not meant to be merged. I use them to launch the CI for my changes and make sure my PRs are ready before I open them in `@elwayman02`'s repository. That's not something I _must_ do really, it's just my writer syndrome: I let you read the book once it's ready to be read, and same goes for my PRs.

When you start to create PRs in a forked repository, you need to pay attention to the base branch: the PR can target the main branch in _your_ own repository or in the _original_ repository. As far as I know, if you open the PR on _your_ repository, you can't edit the base branch later to make it target the original repository. What you have to do is to create a second PR with the "New pull request" button on the PRs tab. You can then target the main branch of the original with the custom branch you have been working on.

Lastly: don't be afraid. A PR is a request by design. Even if you open something somewhere by mistake, the world will be ok.

<br />
<br />

_Maximizing my impact on the Ember Initiative with so little time allocated to it is quite challenging, but I did my best at it. I reworked our [public project board](https://github.com/orgs/mainmatter/projects/14) to make it more aligned with our "continuous improvement" organization that replaced the quarter, and I used different tabs to communicate the priorities. I also opened a few PRs to improve our dear `ember-vite-codemod`, and I started to get involved in `ember-scroll-modifers` conversion to v2. I should be able to move forward a bit next week as well._

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md), 
[Big break](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/big-break.md)
