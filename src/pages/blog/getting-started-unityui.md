---
title: "Getting started with Unity UI toolkit"
excerpt: "UI Toolkit is the new way to create user interfaces. It replaces the Unity UI (uGUI package)."
publishDate: "2023-08-25T15:36:19.399Z"
image: "https://miro.medium.com/v2/resize:fit:630/1*cFd_PsU0nxlOI-g_Y26Xtw.png"
category: "Game dev"
author: "Braulio Camarena"
layout: "@layouts/BlogLayout.astro"
tags: [unity ui, unity, ui toolkit]
---

UI Toolkit is the new way to create user interfaces. It replaces the Unity UI (uGUI package). It based on standard web technologies. Today you will explore the capacities and you will start understanding the basic concepts to start using the power of standard web formats.

## Overview

Chances are that you have been struggling with the old UI system, even though some games do not need a scalable way to create a user interface, sometimes you need to face the problem of create complex UI systems.So, Unity now offers a new way that will help you in these special cases.

UI Toolkit is mean to be used as the recommended UI system and is installed by default since Unity 2021 LTS. It has a different approach where the UI is separated from the scene. Now you create UI Documents (UXML), and Stylesheets (USS), all these with the help of the UI Builder window. It allows you to visualize, create and modify a UI Document on the fly.

## Creating a UI Document

To create a new document in the hierarchy window, only use left click and select UI Document that is inside UI Toolkit.

This will create a Game Object with a UI Document component attached.

![ui document.](https://miro.medium.com/v2/resize:fit:289/1*dd7ocnSvMmmze8XLtD9tdg.png)

Now it's time to open the UI Builder that will create a UXML and USS file.

## UI Builder

![ui document.](https://miro.medium.com/v2/resize:fit:447/1*gykI6xY4jB7NNjuVXW0OGw.png)

![ui document.](https://miro.medium.com/v2/resize:fit:630/1*XF4mXFxJibNcqFWlMfKYJg.png)

To Open the UI Builder, in the window tab search for UI Toolkit and select the correct option.

The currently open and active UI Document (UXML) asset name is displayed in both the Hierarchy pane as a root tree item as well as in the Canvas header inside the Viewport. An asterisk \* next to the name indicates unsaved changes.

As you can see you will notice the next sections:

### Inspector

The inspector has the same functionality as the one of the Unity Editor, it´s used to show the properties and options of the elements selected, a Visual Element will show the attributes, stylesheet and inline styles.

Inside the Inline Styles you will be most of the time changing the different properties. Each saved change will be reflected inside the UXML code of the document

![ui document.](https://miro.medium.com/v2/resize:fit:277/1*xTKO1lRQ9slOCLXVSBA9PA.png)

### Viewport

Within the viewport section you can see the canvas, a container that will allow you to edit a live version of the Document (UXML). You can resize the Canvas inside the section by dragging its edges or corners. Here you be able to add different kinds of containers, controls and fields.

Remember that we are working with separates files, here you can preview the UMXL and USS files where you can open with you preferer editor and start editing manually.

![ui document.](https://miro.medium.com/v2/resize:fit:630/1*C9kRmTlpLemGlLv0I5Pl0w.png)

Inside the inspector you can change the canvas size manually or match with the game view. The second can be really useful for see the correct iteration of the UI process.

Also, you can change the canvas color, use an image or the camara view as background. Notice that can toggle the Editor Extension Authoring to enable work with the Editor UI in case that you are developing an editor extension.

![ui document.](https://miro.medium.com/v2/resize:fit:270/1*XyIJqLLFv5U1BZyWIacTsw.png)

### Hierarchy

The hierarchy is the overview of the document tree, there you will notices as root the UXML file. Here you can drag a drop element from the library.

## Stylesheets

The stylesheets sections is where all your selectors are displayed. You can add selector by writing the name on the input and clicking the plus button.

If you have worked with CSS you will noticed that a USS selector is almost the same but simpler, by clicking the USS file you will see instrucción to apply the style to the desired elements.

![ui document.](https://miro.medium.com/v2/resize:fit:272/1*CCmBRc1vMFde5wVfjGRkDA.png)

Once added a selector you can start changing the style inside the inspector. One important thing is that we create Documents with the power of Flex Box, a system that was designed to improve the distribution and align capacities.

Here is used the box model that is essentially a box that wraps around every HTML element. It consists of margins, borders, padding, and the actual content.

![box model.](https://miro.medium.com/v2/resize:fit:630/0*Y7ADer-FvcNFqXph.png)

### library

Inside the library we will find two tabs **Standard** and **Project**. Inside the first you will see the containers, controls and numeric fields. Inside the other you will use another UI Document created.

The containers section has all the different components that will help you to group UI elements. The Visual Element is like an empty Game Object or Div in html. The other components are kinds of views.
![box model.](https://miro.medium.com/v2/resize:fit:167/1*3lU7x0EFBWmZ_GoztAKgPw.png)

Inside the controls section you will find the most of elements needed to build a user interface like Buttons, Tex fields and Inputs.

![box model.](https://miro.medium.com/v2/resize:fit:512/1*7GaHbWO08Whs5KFdMkb5sg.png)

The final part is for Numeric Fields where you can search for different kinds of Input related to all numeric values needed including advanced ones like Vector 4.

![box model.](https://miro.medium.com/v2/resize:fit:507/1*KAFRJJLQ9IjKaxiJVlM3EA.png)

As you can see almost everything that you need to create a user interface is inside the Standard Tab, but what if i what to reuse another UI Document? The Project Tab is where you can search for other Components created by yourself and include it as UI Document in the hierarchy.

## Implementing Code

Now It is time to add some functionality to a User Interface. First remember to add the UI Document with the decided Source Asset, in this case “GameOverLayout.xml” a simple UI Interface with a button.

![box model.](https://miro.medium.com/v2/resize:fit:283/1*itY5SmuwHXmqAdylpppLeg.png)
![box model.](https://miro.medium.com/v2/resize:fit:470/1*p72dUOtGFC53sGBjYXe9kg.png)

Now you should add a id to the button, this is the way to start programming because we will need a reference of the button.

The code above shows the implementation of a restart button, once clicked the Restart Button the Scene Manager will load the current scene. Note that we need the Unity.UIElements scope to reference a UIDocument, At the
Start function we get the root visual element where will be reference the button using a generic function that accepts as parameter the decided id assigned before.

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using UnityEngine.UIElements;

public class LevelCompletedUI : MonoBehaviour
{
    [SerializeField] private UIDocument _uIDocument;
    VisualElement root;
    void Start()
    {
        root = _uIDocument.rootVisualElement;
        Button buttonRestart = root.Q<Button>("RestartButton");

        buttonRestart.clicked += () => Restart();
    }
    public void Restart()
    {
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }

}
```

# Conclusion

Creating user interfaces with unity used to be complicated at the moment of creating complex UI systems, now with Unity UI Toolkit adopts a tested way with the power of web standards.
