---
title: "Getting started with Firebase Emulator Suite"
excerpt: "The new Firebase Emulator allow you manage a firebase project inside your own local environment."
publishDate: "2023-08-04T15:36:19.399Z"
image: "https://miro.medium.com/v2/resize:fit:630/1*pCuwNTu1PZfvzGYzJwRt3A@2x.png"
category: "Firebase"
author: "Braulio Camarena"
layout: "@layouts/BlogLayout.astro"
tags: [firebase, local enviromment, firebase emulator suite]
---

The new Firebase Emulator allow you manage a firebase project inside your own local environment. This can be really useful when you need to try your apps features, also you do not want to mess around with production. So Firebase Emulator should be the way to go at developing Apps with Firebase.

# Installation

To install the Emulator suite make sure to have the next:

> Node.js with version 16.0 or upper.

> Java Development Kit 11 or upper.

Now follow the next instructions to install the suite.

1. Install Firebase CLI, you will need a version 8.14.0 or superior.

```bash
npm install -g firebase-tools
```

Execute the next command to verify the installed version.

```bash
firebase --version
```

Now login into your account using the next command:

```
firebase login:ci
```

This will make you appear a browser window where your google account must be introduce.

2. Now It’s time to initialize a new Firebase project with:

```bash
firebase init
```

The script will ask you to proceed, just enter “y”. Now you will need to select the option Emulators: Set up local emulators for Firebase products.

After that you can select an existing project, or create new. But in this case don’t set up a default project is selected.

3. The next step is to select the emulators. make sure to select the ones that you want in case that you need to start select other after configuration or you already initialized a project you can start from this step with the next script:

```bash
firebase init emulators
```

At the final part you can choose the ports of each feature. In this case default values are selected.

After installation process in completed a message will appeared, noticing the creation of firebase.json and firebaserc config files.

## Configuration Process

The firebase.json contains the configuration of the emulators, where the port is specified. you can change these values in required case.

```json
{
  "emulators": {
    "auth": {
      "port": 9099
    },
    "functions": {
      "port": 5001
    },
    "firestore": {
      "port": 8080
    },
    "storage": {
      "port": 9199
    },
    "ui": {
      "enabled": true
    },
    "singleProjectMode": true
  }
}
```

Inside package.json is nescesary to add the functionality of start the emulator with a “seed”, a folder generaded once the export command is executed, this will allow you to export all the data that is inside the emulator suite. This is meant to be a important feature because now you can mess around with the functionality of your app.

```json
scripts: {
    "dev": "firebase emulators:start --import=seed",
    "export": "firebase emulators:export seed",
}
```

## Conectig App to Emulator

At your firebase config file, you can initialize and connect to the emulators. Notice that you should add logic to allow only connect to emulators on the development eviroment, with Node js you can add this logic with the process.env.NODE.ENV variable, where should be equals to “development”.

```javascript
import { initializeApp } from "firebase/app";
import { getFirestore, connectFirestoreEmulator } from "firebase/firestore";
import { getAuth, connectAuthEmulator } from "firebase/auth";
import { connectStorageEmulator, getStorage } from "firebase/storage";

interface FirebaseConfig {
  apiKey: string;
  authDomain: string;
  projectId: string;
  storageBucket: string;
  messagingSenderId: string;
  appId: string;
}
const config: FirebaseConfig = {
  apiKey: "...",
  authDomain: "...",
  projectId: "...",
  storageBucket: "...",
  messagingSenderId: "...",
  appId: "",
};
const authUrl = "http://127.0.0.1:9099";

const app = initializeApp(config);
export const storage = getStorage(app);
export const auth = getAuth(app);
export const db = getFirestore(app);

if (process.env.NODE_ENV === "development") {
  connectAuthEmulator(auth, authUrl);
  connectFirestoreEmulator(db, "127.0.0.1", 8080);
  connectStorageEmulator(storage, "127.0.0.1", 9199);
}
```

## Firebase Emulator UI Overview

Once used the firebase emulators start command now you can access to the Emulator UI, there you will notice the change of a purple like theme. This is meant to be clear that your are running in a development safe environment.

Inside the overview tab you can see the different emulators , with the respectives ports and status.

![emulator suite](https://miro.medium.com/v2/resize:fit:630/1*TGomZ5496Qwj4Sbq6ujI2A.png)

In this example Authentication, Firestore and Storage are enabled. You will noticed some changes to the production version, like the clear all data button. But do not worry about it, remember to use firebase emulators:export seed that will create the seed folder inside your project and all you data will be saved.

![emulator suite](https://miro.medium.com/v2/resize:fit:630/1*WLdgl3FRS-RmA9UIPXyovg.png)
![emulator suite](https://miro.medium.com/v2/resize:fit:630/1*3TGi6ygH_wVtMZSyxbiOcQ.png)
![emulator suite](https://miro.medium.com/v2/resize:fit:630/1*J6B5MHV_80PeL1F9G8QrJQ.png)

One important tab is the one named “Logs” where you can check all activity made. This is really useful at time to find query leaks.
![emulator suite](https://miro.medium.com/v2/resize:fit:630/1*PfShV-udlX9rQGdVb0wW3g.png)


## Conclusión

This is a the first step to use the Emulator Suite, as you can see is really straightforward and it have a lot of benefits. Now is time to start using it in your firebase projects and start messing around without worry.
