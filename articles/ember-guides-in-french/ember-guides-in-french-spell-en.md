# Ember Guides in French 🇫🇷 - Spell-checking the language

This article is part of the "Ember Guides in French 🇫🇷" series that introduces the French translation project for the Ember Guides. If you want to know more about the context, read [the introduction article](./ember-guides-in-french-en.md). The present article will detail how we lint and spell-check the docs markdown files. It is going to be about working with `remark`/`retext` ;)

## Context

Any writer knows that spell-checking is not an option to produce qualitative content. Even people with good writing skills are not always able to see every single mistake they write or read, and even a minimalist spell-checking tool can point out a couple of careless mistakes. A translation project is a great opportunity to dive into this. In our case, it will be about [`unifiedjs`](https://unifiedjs.com/) world specifically.

> unified is an ecosystem for dealing with content as structured data. It consists of 500+ packages to do a wide variety of things. It’s used in 1m+ projects but a well-known example built on these packages is MDX. Maintaining all those projects takes a lot of time, which is why we’re on OpenCollective!
> - https://opencollective.com/unified

To scope this a little bit to our project: `remark` packages are a bunch of packages we are going to use to lint our docs markdown files. `retext` packages are a bunch of packages we are going to use to lint French. And this whole family of packages is maintained by the same guys from `unifiedjs` collective. Especially one guy, [Titus Wormer](https://github.com/wooorm) who - seems to be a huge penguin fan for some reason, and - is very reactive and willing to help on `remark` and `retext` discussion pages.

## Solution

### Setting up a dictionary

- This official Guides also contains a  "local Ember dictionary" that contains extra words related to Ember and tech which don't exist initially in English. We can't reuse it as it is, because we can have only one local dic, and our French dictionary doesn't miss only these Ember words, it also misses a bunch of English words commonly used in French (which exist in the English dic so they're not present in the Ember local dic). 

###  Handling links to articles in English

### Prevent spell-checking on not translated files