# The Ember Initiative Journey 🐹❤️

_Week 1 - the codemod_

_#web #emberjs #codemod #ast #npmView #nodeFs #embroider #vite_

Ember's power is step-by-step improvement. As the framework evolves, the community won't leave you behind: it will provide you with everything you need to update your app and adopt modern practices at your own pace (Trust me on this; the first version I used was a 2.x, and I did all the way to 4.x). My job now is to help you migrate your classic Ember app to build with Vite. This is the first step of my journey: **the codemod to help developers migrate from classic apps to Vite apps**.

## What's a codemod?

A codemod is essentially a script that transforms your code automatically. In the Ember ecosystem, it's a widely used way to help developers adopt a new syntax. For instance, long ago, we wrote double-curlies syntax `{{#my-component}}` to invoke components in a template. Nowadays, we use the angle bracket syntax `<MyComponent>` instead. There is a [codemod that does this for you](https://github.com/ember-codemods/ember-angle-brackets-codemod), so if you need to migrate an old Ember app to the modern syntax, you don't have to do it all by yourself.

## I need to create a codemod; what to start with?

Upgrading a classic Ember app to using Vite requires to move, rename, and change a certain number of files. And since we want the new build system to work from `3.28` to the latest Ember (`6.x` when I am writing this), I expect there will be many cases to handle. The task sounds overwhelming, so here are approaches to start this:

### The happy path

Choose the _perfect_ use case, which could be a good starting point for transforming the code. Perfect can have different meanings depending on your context; for instance, it could mean "most standard".

🐹 For the classic-to-Vite codemod, the perfect case would be a brand-new empty app generated with `ember new` and initialized with the latest version of Ember. This means the app is completely up to date with modern practices and doesn't have any customization, so it's the most basic case I want to handle, then I can keep building up out of it.

### The mirror

Once you have identified the perfect use case, look at it and look at what you want instead. Put the initial code and the result side by side to get a better picture of what you must achieve. 

🐹 For the classic-to-Vite codemod, I am working at the scale of a whole application, so I can use a tool like [Beyond Compare](https://www.scootersoftware.com/). This software can compare entire folders; I can see what files exist on the left and the right, and by clicking on a file, I have the content diff. It's a very practical approach: you run your codemod in the app displayed on the left, you refresh Beyond Compare, and if there is no more diff (or let's say expected diff only), then you win. Combine this with `git` and a custom `reboot` command that resets the state of the left side to HEAD, and you have a good enough development workflow. 

<img width="1483" alt="codemod-story-compare" src="https://github.com/user-attachments/assets/0cd8b8af-4f5c-4892-9d6b-bb0cf85df16e" />

### The transform

Once you have a good vision of where you are and where you want to go, you must decide the best way to transform the code. Here are a few leads.

- **A simple text replacement**: If your use case is somewhat "static", and you want to turn very specific strings into other strings, then maybe you can go with basic JavaScript functions like `replace` and `replaceAll`, and why not look at `RegExp` (regular expressions) as well.

- **The AST structures**: An [Abstract Syntax Tree](https://en.wikipedia.org/wiki/Abstract_syntax_tree) is a data structure representing a program as a nodes tree. If the piece you want to transform is embedded into complex and potentially customized code, and the way to identify it relates to the code grammar, then this is the way to go. The tool [AST Explorer](https://astexplorer.net) is a "must-use" to work with AST, you can copy-paste any valid code there and select the parsers you use to see the corresponding AST. If you are a beginner, this [Babel Plugin Handbook](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/en/plugin-handbook.md#toc-introduction) has good explanations (Babel is just one tool relying on AST, but the principle can apply to other contexts like ESLint rules, etc). [recast](https://github.com/benjamn/recast) is one lib you can use to edit your code using AST (1 - read the file with node fs, 2 - parse with recast, 3 - manipulate the AST with recast, 4 - print AST with recast, 5 - rewrite the file with node fs). 

- **Git commands**: This insight is more about initializers than codemods. If you expect your users to work with git, there are also ways to explore here. `git diff` and `git apply` allow you to print a diff between two files and try to apply a patch. Investigating how frameworks and lib initializers prompt you for blueprint options and offer to edit when your existing files conflict with the blueprint can be something to investigate.

🐹 For the classic-to-Vite codemod, I'll probably use a mix of text replacements and AST manipulations.

## Other tips

- The command [`npm view`](https://docs.npmjs.com/cli/v7/commands/npm-view) allows you to print information from packages publicly published on npm. If you need to check a dependency for updates, that's an easy way to retrieve the information. 🐹 For the classic-to-Vite codemod, I use it to check if the latest version of a v1 addon is a v2 (using the meta 'ember-addon' from the package.json).

- If you work at the scale of a whole folder, you may need to use node filesystem. Two features to know are [`process.cwd()`](https://nodejs.org/docs/latest/api/process.html#processcwd) and [import.meta.url](https://nodejs.org/docs/latest-v15.x/api/esm.html#esm_import_meta_url). The first one will help you retrieve from where the node process is executed, and the latter what module you are currently in when its code executes. Let's assume I run the codemod in the app folder I want to transform:
```js
// my-codemod/index.js
import { readFile } from 'node:fs/promises';
import { dirname, join } from 'node:path';
import { fileURLToPath } from 'node:url';
const __dirname = dirname(fileURLToPath(import.meta.url));
const pkg = JSON.parse(await readFile(join(__dirname, 'package.json'), 'utf8'));
// pck is the package.json of the codemod app

// my-codemod/some-feature.js
let path = join(process.cwd(), 'config/environment.js')
// path point to my-app-to-transform/config/environment.js, because I run the codemod in my-app-to-transform folder
```

<br />
<br />

_At the end of the week, I explored things that will turn out to be reworked or unused; alas, this is the way with this kind of project. I think a part of my work is valid though, especially the text replacements on the index.html files and the AST transformations on ember-cli-build.js and app.js. I'll need another week to get my "perfect case" working the way it needs to work._
