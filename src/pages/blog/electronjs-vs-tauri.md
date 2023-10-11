---
title: " Using Vite with Ionic React"
excerpt: "Make desktop apps using web technologies can be tricky, so there was a framework that used to dominated the game Electron."
publishDate: "2023-08-01T15:36:19.399Z"
image: "https://miro.medium.com/v2/resize:fit:630/1*GeJiIwfC1EbzxpukTZLF6g.jpeg"
category: "Web Dev"
author: "Braulio Camarena"
layout: "@layouts/BlogLayout.astro"
tags: [tauri, electronjs, webdev,]
---

Make desktop apps using web technologies can be tricky, so there was a framework that used to dominated the game Electron. Now electron have some performances issues and a new option appeared, Tauri a frontend-independent application made using rust. However, electron seems to be the most popular option.

## Overview

Electron have a great developer experience, it uses node js as backend making posible the use of native Apis. It uses Chromium to render the view, so you will need that space in disk even though you just need to show a “hello word”.

Tauri uses another approach where the performance is the key. It uses Rust as a backend and from the fronted the libraries Tao and Wry to provide a lightweight WebView. The Tauri api provides a secure way to access native functionality and is secure by default.

# Getting Started With Tauri

First you should install Rust and Nodejs and create a new Tauri app.

> npx create-tauri-app

When the app is created you will notice the familiarity with a web project, but with the difference of the “src-tauri” folder, where you will find files related to the rust ecosystem, like the cargo.toml the config file for the package manager cargo. Also, Tauri config files like tauriconf.json, where you can change several options related to the build of the program.

The entry point of the backend is located at the src folder with the main.rs file. From this you can customize the experience from the native operative system. The most important is that there you can invoke commands that can be called from the JavaScript frontend and it have its own even systems that allows complex messages patterns to the frontend to the backend.

In the frontend code a vast of native Apis can be accessed. for example, write file. where the user is able to create a file at the hard drive.

```javascript
import { writeFile, FSTextFileOption } from "tauri-apps/api/fs";
const handelClick = async () => {
  const f: FsTextFileOption = {
    path: "./test.txt",
    contents: "file content",
  };
  await writeFile();
};
```

Access any api methods can be allowed inside the allow list atribute at Tauri conf.json. Remember that Tauri is secure by default.

```javascript
"allowlist":{
  "fs":{
  "all":true.
  "readFile:":true,
  "writeFile":true.
  "readDir": true,
  "removeFile": true,
  "renameFile": true,
}
```

To compile and build the app you can run the npx tauri build command, this will create a executable in the target directory.

## Getting Started with Electron

The way to use electron is first create a empty directory where the project will be located, the run:

```bash
npm init -y
npm install electron -D
```

Then create a main.js that will be the entry of your app, every electron app have one main process running it manages the cycle of the app. When the main process is ready you can instantiate a new window to load the frontend. It will render the html, css and javascript and give you access to the native Apis. As example I will use a plain html file.

```javascript

const {app, BrowserWindow} = require(‘electron’)
app.whenReady().then(())=>{
  const myWindow = new BrowserWindow({
    with: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true
    }
});

myWindow.loadFile('index.html');

```

Create a new html file and put whatever code you want inside of it. now you once you run the app with “npm run electron” and you will notice that a new window appeared with the html content.

Now you can build your app installing electron-builder adding to next script:

```json
"package": "electron-builder build"
```

Note that electron is just a library and use you should have knowledge to start implementing the app, there are useful tools to scaffold the app like electron forge the all-in-one tool for packaging and distributing Electron applications.


## What is the best option? 
Both Tauri and Electron have it strengths and drawbacks, in the first side we have the performance and security vs the use of a common tool for web developers like node js. Both provide a great developer experience a great set of tools for the native functionality. Tauri is more like a complete framework with a set of conventions and cli tools, in the other hand. Electron is more like a library that provides a bridge between node and chromium.

For me the decision is clear electron is still the best option for the familiarity of tools, Rust have the power but not the commodity that offers a always used runtime. Speaking about the best tool Tauri is one step ahead but still there is one king.