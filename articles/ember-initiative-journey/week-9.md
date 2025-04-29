# The Ember Initiative Journey 🐹❤️

_Week 9 - a plan for Ember Inspector_

_#web #emberjs #docs_writing #ember_inspector #vitejs #embroider #virtual_files_

This week was a lonely week for me since both my coworkers and my manager were on vacation. I had to move forward with all the topics we had on the table, and I focused on three of them: improving ember-vite-codemod, preparing the communication about the Ember addons audit, and working on Ember Inspector.

## First things first: rewrite the README

Like every senior developer, I was a junior once. My most traumatising memories from this period relate to a particular part of error solving: guessing what other developers mean when they write stuff on the Internet. At some point, it seemed to me that they were unclear _on purpose_, I was suspecting some unconscious ego issue, like "If I add more detailed explanations about something, it means I think it's not obvious. But if other developers think that I think it's not obvious, but it's obvious to them, then they will think I am incompetent". Something like that. I was desperately seeking a logical answer to the questions: "Why are all your docs so BAD? Why don't you want to EXPLAIN? You've written a lot of stuff here, but what's the CONCLUSION? What do you MEAN? What's the matter with YOU?".

Almost a decade later, I am no longer that mad at the entire dev community. The main reason is that I learned enough things to understand way more often what they try to say, and I can generally follow the docs from A to Z 🎉 But I still struggle sometimes. Now, even on docs that look globally pretty good to me, each time I don't understand a line right away, each time I have to experiment a bit to reach the "ah, ok, that's what they mean"... I have an emotional thought for the junior me who would have just thrown her computer through the window and given up everything to go breed a herd of goats in the Ardèche hills. And I rewrite the docs.

You only have good reasons to rewrite the docs:

- It's the easiest type of open source contribution. You just change a markdown file, it's 100% safe, you're not going to break the world.
- If you didn't understand something immediately, there are certainly other developers who won't understand it at all. Your feedback has value, and if someone answers you, "Pff, but that's obvious," then this person is the problem; you're not the problem.
- If you don't like helping other people that much (it's fine), then help yourself. The next person reading this document after you could be you, eight months later, without any recall of what was it you struggled with.

In short, I opened a PR to improve ember-inspector README.

## Ember Inspector 

After digging a bit into the Ember Inspector code, Chris (`mansona` on GitHub) and I drafted a more accurate plan.

- **Proof of concept**: Implement a rough Vite support using code changes in `ember-inspector` and `ember.js`. In a nutshell, the inspector side needs to read a new object provided by the Ember side because it can no longer rely on AMD modules and Ember barrel file, which is deprecated. This is already done; Chris opened two draft PRs in each repository and got it to work.
- **Quick fix**: Including changes in `ember.js` is a long process involving writing an RFC to design and discuss the final solution. Meanwhile, Vite users are stuck with a non-functional inspector. To solve that problem, we want to implement a temporary solution using Embroider's virtual file system. We want to make Embroider able to return the content ember.js should provide to the inspector at some point. That's what I explored this week, I have a draft PR on Embroider repo that partially runs but still requires work.
- **RFC**: Based on the proof of concept, write an RFC to describe the new protocol for the inspector to communicate with `ember.js`.
- **Inspector Implementation**: out of the proof of concept, continue to dig into the inspector code to understand what’s still missing, what can be cleaned up, what the concept of locking versions exactly is… and obtain the final PR to implement Vite support.

One thing I wasn't expecting, though, was how complicated it would be to try out Chris' prototype. To get it to work, you must have both of his branches (the ember.js side and the ember-inspector side) running together. In other words, you need to [pnpm link](https://pnpm.io/cli/link) the `mansona/ember.js` branch to some Ember app you want to inspect, serve that Ember app, run the `mansona/ember-inspector` branch locally, and execute the script to load that local inspector in the app you are serving. It would have been doable without those obscure Ember errors I get with my ember.js link, and unfortunately, I can't document the learnings in this weekly log since I haven't figured out the answer yet.

<br />
<br />

Not the easiest week ever, there was a lot of context switching, but in the end I am rather satisfied with the outcome: four improvements delivered on ember-vite-codemod, a draft for Ember Inspector to continue when Chris is back, and a blog post in preparation about the addons audit that could be realistically published by the end of next week. Let's see if week 10 can be the release of our temporary Vite support for the inspector.

<br />

[Intro](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/intro.md), 
[Week 8](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-8.md),
[Week 10](https://github.com/BlueCutOfficial/BlueCutOfficial/blob/main/articles/ember-initiative-journey/week-10.md)
