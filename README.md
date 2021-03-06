# md2cwm

> This is a fork form [Shogobg/markdown2confluence](https://github.com/Shogobg/markdown2confluence), Thanks for `Shogobg` to provide such goof util and i wanna do some refactors with markdown ast utils.

This tool converts [Markdown] to [Confluence Wiki Markup].

## Installation

```sh
npm i -g md2cwm
```

```bash
npm i --save md2cwm
```

## Command-Line Use

Read in Markdown files and allow to use glob

```bash
md2c *.md <path/to/docs>
// md2cwm the same
```

## As library dependency

Now you write some JavaScript to load Markdown content and convert.

```javascript
const md2cwm = require('md2cwm');
const markdown = fs.readFileSync('README.md');
const confluence = md2cwm(markdown);
console.log(confluence);
```

This uses the wonderful [marked](https://www.npmjs.com/package/marked) library to parse and reformat the Markdown text.

## Custom options

Since this tool uses [marked](https://www.npmjs.com/package/marked), there is a pre-defined renderer which we pass to [marked](https://www.npmjs.com/package/marked).
If you want to replace any of the predefined functions or the renderer as a whole, you can do so by passing an options object to the tool.

```javascript
md2cwm = require('md2cwm');
markdown = fs.readFileSync('README.md');
confluence = md2cwm(markdown, {
  renderer: {
    link: href => {
      return `http://example.com/${href}`;
    },
  },
});
console.log(confluence);
```

Additionally, the options objects takes custom arguments for the confluence code block options.

```javascript
md2cwm = require('md2cwm');
markdown = fs.readFileSync('README.md');
confluence = md2cwm(markdown, {
  renderer: {
    link: href => {
      return `http://example.com/${href}`;
    },
  },
  codeBlock: {
    // Adds support for new language
    languageMap: {
      leet: '1337',
    },
    // Shows the supported options and their default values
    options: {
      title: 'none',
      language: 'none',
      borderStyle: 'solid',
      theme: 'RDark', // dark is good
      linenumbers: true,
      collapse: true,
    },
  },
});
console.log(confluence);
```


