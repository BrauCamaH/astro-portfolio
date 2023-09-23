---
title: " Using Vite with Ionic React"
excerpt: "Create React App is part of the past, nowadays there is a tool that dominates, Vite is the next generation frontend tooling for excellence. Today I will show you how to migrate your Capacitor app for React."
publishDate: "2023-07-24T15:36:19.399Z"
image: "https://miro.medium.com/v2/resize:fit:630/1*mTqU7Rw1luq_uxC3OEh4ug.png"
category: "Web Dev"
author: "Braulio Camarena"
layout: "@layouts/BlogLayout.astro"
tags: [webdev, vite, ionic]
---

Create React App is part of the past, nowadays there is a tool that dominates, Vite is the next generation frontend tooling for excellence. Today I will show you how to migrate your Capacitor app for React.

First you should install Vite and remove React Script.

```bash
npm install vite
npm remove react-scripts
```

Now update package.json by changing the start and build command. Also is recommended to add the serve and sync scripts.

```json
"scripts": {
    "serve": "vite preview",
    "start": "vite --host",
    "build": "tsc && vite build",
    "sync": "npm run build && ionic cap sync --no-build",
  },
```

Once finished you must change the index.html file from the public folder to the root of the project, and update with the content bellow.

```html
<!DOCTYPE html>
<html lang="en">
 <head>
 <meta charset="UTF-8" />
 <link rel="icon" type="image/png" href="/assets/icon/favicon.png" />

 <meta name="viewport" content="width=device-width, initial-scale=1.0" />
 <title>Your App</title>
 </head>
 <body>
 <div id="root"></div>
 <!-- Add entry point 👇 -->
 <script type="module" src="/src/index.tsx"></script>
 </body>
</html>
```
Note that at link you should match with your image path in this case favicon.png located at public/assets/icon.

Now It is time to add some config files, you should add the vite.config.ts where the outdir is set to “./build”

```javascript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

// https://vitejs.dev/config/
export default defineConfig({
  build: {
    outDir: "./build",
  },
  plugins: [react()],
});
```

Make sure to modify the tsconfig.json. Also include a tsconfig.node.json.

```javascript
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

```javascript
import { defineConfig } from "vite";
{
  "compilerOptions": {
    "composite": true,
    "skipLibCheck": true,
    "module": "ESNext",
    "moduleResolution": "bundler",
    "allowSyntheticDefaultImports": true
  },
  "include": ["vite.config.ts"]
}
```

Finally add the vite.env.d.ts file.

```javascript
/// <reference types=”vite/client” />
```

Now you are using the power of Vite, and you have noticed the fast that you are ready to start coding.
