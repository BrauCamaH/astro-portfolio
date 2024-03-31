---
title: "Using Vim with VS Code"
excerpt: "AR Chair is a augmented reality app where you can visualize a chair"
publishDate: "2024-03-01T15:36:19.399Z"
image: "https://miro.medium.com/v2/resize:fit:640/format:webp/1*gl-fUTuoAcaGuu0AEe92Wg.png"
category: "Editor"
author: "Braulio Camarena"
layout: "@layouts/BlogLayout.astro"
icons: [logos:vim, devicon:vscode]
tags: [vim, vscode, productivity]
---

Visual Studio Code is the preferred text editor nowadays. Vim is an amazing way to edit your code without touching your mouse, so why not have the best of both worlds? Chances are that, now you are using VS Code and you know about how Vim can increase your productivity when writing code. Here you will understand how to integrade Vim into VS Code and enhance the way that you write code.
Vim Plugin for Visual Studio Code

You can start using the power of Vim, just installing the VS Code extension. Once installed and enabled you will notice some changes in the editor.

![vim](https://miro.medium.com/v2/resize:fit:640/format:webp/1*y3Wl5T6B-7tLf3XwcoJ6pw.png)
You will notice that the cursor has change and bellow yo will see “NORMAL”, this is because Vim has different modes. being normal the default.

To start writing code you should type “i” and enter the insert mode. now I will be an explanation of each mode.

## Normal Mode

Here you must use hjkl to move the cursor, where:

> h=> left

> j => down

> k =>right

> l =>left

## Insert Mode

You can start writing code by using the key “i”, when you are in normal mode. Also, you can use “a” to start at one character beyond the cursor. Also:

> I => Enter insert mode at the beginning of the line.

> A=> Enter insert mode at the end of the

## Visual Mode

In this mode you will be able to select the text when you move through the file. To enter this mode, you should only type “v”.

> V => Enter line-wise visual mode.

> <ctrl-v> Enter block-wise visual mode.

> y=> Copy.

> p=> Paste.

> d => Delete.

> c=> Delete and enter in insert mode.

## Execute Mode

Here you will able to insert different commands that will allow you to write, close, and search and many other. Between the most commons are:

> q=> Quit file.

> q!=> Quit file without saving.

> w=> Save file.

> only=>Close all other editor windows.

> tabo=> Close all other tabs.

> /{pattern} Search forward in the file.

> ? {pattern} Search backwards in the file.

This is a short overview of the different modes and commands, everything with vim comes with research and practice. It can be overwhelming at start but with patience you will see the results.

## Customising the Vim Extension

You can customize The Extension to create your own custom behavior, like as you have noticed you cannot use properly <ctrl-c>, <ctrl-p> the first to copy and the second to search for file as normal. You can fix this in settings.json adding the next. line.

```json
"vim.handleKeys": {
    "<C-c>": false,
    "<C-p>": false
},
```

Also, you can create your own key bindings for each mode, mapping a <leader> key, this for example in normal mode it can really be useful, for example.

```json
"vim.leader": " ",
  "vim.normalModeKeyBindings": [
         {
      "before": ["<leader>", "+"],
      "commands": ["workbench.action.increaseViewSize"]
    },
    {
      "before": ["<leader>", "-"],
      "commands": ["workbench.action.decreaseViewSize"]
    },
    {
      "before": ["<leader>", "t"],
      "commands": ["workbench.action.terminal.toggleTerminal"]
    },
    {
      "before": ["<leader>", "f"],
      "commands": ["editor.action.formatDocument"]
    },
  ],
```

Now you can at Normal Mode first press “space” and after that “f” and you will be able to format the entire file, this is easier and more natural that using than normal <alt-shift-f> shortcut. Note that in the example the ability to increase and decrease the view size have been added by pressing “+” or “\*” after the leader key.

Another concern about using Vim with VS Code is the overwhelming use of ESC to change to normal mode this can be fixed with mapping MAYUS TO ESC. Just to keybindings.json and paste the next code:

```json
  {
    "key": "capslock",
    "command": "extension.vim_escape",
    "when": "editorTextFocus && vim.active && !inDebugRepl"
  },
  {
    "key": "escape",
    "command": "-extension.vim_escape",
    "when": "editorTextFocus && vim.active && !inDebugRepl"
  },
```

Conclusion

Now you can start using Vim inside VS Code, I have found this approach amazing for navigation through files, for me this is my best option to write code because you can use a widely use and adopter code editor with the power of vim key motions.
