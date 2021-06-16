---
name: "Guide SDK"
---

# Guide SDK

## Getting Started

The **Guide SDK** is a feature designed to allow developers the ability to integrate their own features with the Guide application. With the SDK, you can trigger certain behaviors, access variables, and react to events as users utilize Guide within your application.

### Start-up

Guide is loaded onto the page via an HTML `<script>` tag. Once the application is loaded, it will initialize the **SDK** on the page, and make itself available for access.

Due to the nature of web browsers, the _order_ of scripts being loaded cannot always be guaranteed. Therefore, developers need some way to ensure their scripts only run _after_ the SDK is made available.

To accomplish this, we can leverage some built-in behavior of the SDK:

```js
function exampleFunction() {
  // Your code here
}

window.GuideSDKInit = exampleFunction;
```

In this example, `exampleFunction` is guaranteed to only execute _after_ the SDK is available. Although this assignment may occur before Guide even runs, it's not yet executed but instead simply set to `GuideSDKInit` on the window.

When the Guide script does run, it will check to see if `GuieSDKInit` exists. If so, it will execute the custom function.

> _Note: `window.GuideSDKInit` can also be an *array* of functions; see API reference below._

In general, **any time you want to interact with the SDK at start-up your code should be wrapped in a function like the one above** to ensure proper timing and availability.

If you would like to perform the above logic from _within_ an asynchronous script, or find yourself in another situation in which the SDK could already be initialized, it may be helpful to perform a conditional check to decide how to invoke your script:

```js
if (window.GuideSDK) {
  exampleFunction();
} else {
  window.GuideSDKInit = exampleFunction;
}
```

<hr>

### Triggering Actions

One feature of the SDK is to allow developers to trigger various Guide actions with their own scripts.

Let's suppose I'm a website developer and I want the Guide window to automatically open upon page load. For this purpose, we can utilize the `openWindow()` function:

```js
function exampleFunction() {
  window.GuideSDK.bot.openWindow();
}

window.GuideSDKInit = exampleFunction;
```

First, we create and bind an `exampleFunction` to ensure proper timing _(see above)_. Within that function, we have a call to the `openWindow()` function, which is located within `GuideSDK.bot` on the `window` object.

Once the SDK is initialized, it will execute our function and the Guide window will be immediately opened.

<hr>

### Reading values

Several values are exposed through the SDK which can be used to perform actions and make decisions in your code:

```js
const activeConversation = window.GuideSDK.bot.activeConversation; // get the ID of the current conversation (if applicable)

if (activeConversation !== undefined) {
  console.log("conversation is active!");
} else {
  console.log("conversation is inactive!");
}
```

<hr>

### Listening for events

If we want to react to certain actions that occur within Guide (e.g. a user starts a conversation), we need a way to listen for the events emitted by Guide.

Let's look at a case where we'd like to log the contents of a message to the browser every time one is sent through Guide:

```js
function logMessage(message) {
  console.log(message);
}

window.GuideSDK.on("sendMessage", logMessage);
```

Now every time the user sends a message through Guide, the SDK will call `logMessage` and provide it with the contents. The contents will then be logged to the developer console.

If we'd like to cease this behavior at a later time, we could then run:

```js
window.GuideSDK.off("sendMessage", logMessage);
```

This will remove the event listener, and the messages will no longer be logged.

<hr>

### Styling the Guide application

In some cases, we may wish to modify certain aspects of Guide's appearance to better match the surrounding website. The entire Guide application is contained within a [ShadowDOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM), **so traditional methods of styling will not work**. Instead, we can accomplish custom styling using the SDK's styling features.

Let's look at an instance where we'd like to color all `<p>` elements with the color red:

```js
const myStyle = `
  p {
    color: red;
  }
`;

window.GuideSDK.bot.style.add(myStyle);
```

First, we create a normal string that contains our desired CSS styling. In this case, we simply target the `<p>` elements and color them red. Then, we provide the string to the `style.add()` function, which injects it into the DOM and the browser applies the style.

> _Note: References to `<style>` and `<template>` elements are also accepted, see API documentation._

For a more concrete example, we can also see how to re-color Guide's header to green:

```js
const myStyle = `
  div[class^="Header__HeaderWrapper"] {
    background-color: green;
  }
`;

window.GuideSDK.bot.style.add(myStyle);
```

The CSS selector in the above example may be unfamiliar to you, but it simply targets any `<div>` whose `class` value _begins_ with `Header__HeaderWrapper`. **Most of the major discrete components of Guide must be targeted in this manner**; you can read more about why in the styling section below.

## Real-world examples

Using these features, let's look at a couple of examples that combine these functionalities to solve some real use-cases.

### Opening Guide with a button

Let's say I'm a website developer who'd like to create a "Speak to an Agent" button on my website. When clicked, this button should open Guide, and begin a conversation with an available agent.

First, I would create the HTML for the button:

```html
<button onclick="handleClick()">Speak to an Agent</button>
```

Then, the corresponding Javascript function:

```js
function handleClick() {
  const message = "Speak to an Agent";
  window.GuideSDK.bot.sendMessage(message);
}
```

Now when the button is clicked, my `handleClick` function will send the appropriate message through the SDK to automatically begin a conversation with an agent.

<hr>

### Launching Guide via URL

Now, I'd like my site to vary the behavior of Guide based on the current URL so that some users will have the Guide window opened automatically.

For this example we're going to use an `open` [url parameter](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) to differentiate behavior:

`https://myhospital.com/?open=true`

then, within our Javascript:

```js
function checkURL() {
  const currentURL = new URL(window.location);
  const parameters = currentURL.searchParams;

  if (parameters.get("open") === "true") {
    window.GuideSDK.bot.openWindow();
  }
}

window.GuideSDKInit = checkURL;
```

As before, we again define a function for the SDK to execute once it's initialized. Within that function, we parse parameters using the browser's built-in functionality. If `open=true` (as in the above URL), our function will call the SDK causing the Guide window to open.

## Event Listener

The Guide SDK offers an event listener that executes a callback when a predetermined event is fired. To attach an event listener, simply call:

```js
window.GuideSDK.on(eventName, callback);
```

To remove an event listener, you can call:

```js
window.GuideSDK.off(eventName, callback);
```

#### Events

| Event Name        | Payload                         | Trigger                                                    | Example Payload                                               |
| ----------------- | ------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------- |
| conversationStart | conversationId: String          | New conversation is started (only occurs once per session) | `{ conversationId: '1afb23b2-8eb0-4972-8cdc-1cf59cffb540' }`  |
| conversationEnd   | `N/A`                           | Conversation is ended                                      |                                                               |
| messageSend       | message: String                 | Message sent through Guide                                 | `{ message: 'Hello, World!' }`                                |
| messageReceive    | author: String, message: String | Message received through Guide                             | `{ author: 'Scranton Healthcare', message: 'Hello, World!' }` |
| windowOpen        | `N/A`                           | Guide UI window opened                                     |                                                               |
| windowClose       | `N/A`                           | Guide UI window closed                                     |                                                               |

## Bot API Reference

The Guide SDK also has an API that allows developers to interact with the bot directly via the `window.GuideSDK.bot` interface. These API calls can be invoked any time after the bot has been initialized.

`window.GuideSDK.bot.*` in the console

#### activeConversation `property`

ID of the current conversation, if active.

<hr>

#### activeWorkflow `property`

ID of current workflow, if applicable.

<hr>

#### sendMessage(message)

Send message, initiate conversation if necessary.

<hr>

#### startConversation(message)

Initiate conversation with _message_.

<hr>

#### endConversation()

Terminates currently active conversation.

<hr>

#### resetConversation()

Resets the current conversation.

<hr>

#### purgeConversation()

Purge local state for current conversation.

<hr>

#### openWindow()

Open guide window.

<hr>

#### closeWindow()

Close guide window.

<hr>

#### setCustomVariables(config)

##### Example

```js
window.GuideSDK.bot.setCustomVariables({
  custom_first_name: "Radric",
  custom_last_name: "Davis",
  custom_account_number: "12345678",
  custom_birth_date: "07/07/1980",
  custom_phone_number: "770-999-0989",
  custom_email_address: "radric@email.com",
  custom_address_1: "123 Main Street",
  custom_city: "Atlanta",
  custom_state: "GA",
  custom_zip: "30308",
});
```

##### Description

Sets the conversation custom variables that are used to surface patient information to live chat agents.

Note: custom variables collected by form actions will take precedence over custom variables set by the `setCustomVariables` call.

##### Custom Variables

| Variable              | Type   | Example                         |
| :-------------------- | ------ | ------------------------------- |
| custom_first_name     | String | Michael                         |
| custom_last_name      | String | Scott                           |
| custom_birth_date     | String | 03-15-1964 (or 03/15/1964)      |
| custom_phone_number   | String | 555-555-5555                    |
| custom_account_number | String | 1234567890                      |
| custom_email_address  | String | michael.scott@dundermifflin.com |
| custom_address_1      | String | 42 Kellum Court                 |
| custom_city           | String | Scranton                        |
| custom_state          | String | PA                              |
| custom_zip            | String | 18503                           |

<hr>

#### setCustomSettings(config)

##### Example

```js
window.GuideSDK.bot.setCustomSettings({
  padding: 25,
  customClassName: "bot-variant-a",
});
```

##### Description

Sets the bot's custom settings. This list is continuously growing, however we currently only offer two options.

| Key             | Type   | Example        | Description                                                                                              |
| :-------------- | :----- | -------------- | -------------------------------------------------------------------------------------------------------- |
| padding         | Int    | 25             | A number that will define the padding around the Guide launcher/ bot                                     |
| customClassName | String | 'scranton-bot' | A value that will be added to the top level of the React component, allowing the client to run A/B tests |

##### Deprecated

You can also add these settings by setting them to the `window.guideSettings` object, however this is deprecated and may be removed from future versions.

```html
<-- add a script tag in your head to customize your Guide implementation -->
<script>
  window.guideSettings = {
    padding: 25,
    customClassName: "scranton-bot",
  };
</script>
```

<hr>

#### style.add(style)

##### Example

```js
window.GuideSDK.bot.style.add(`
  div {
    font: 15px Arial, sans-serif;
    color: red;
    border: 1px solid black;
  }
`);
```

Inject style into Guide's Shadow DOM.

Styles can be injected in several ways, depending on the type of parameter passed:

##### String

When a string is passed, a new `<style>` element will be created automatically and its contents set to that of the string.

##### <style\>

When a `<style>` tag is passed, it will be directly inserted into the Shadow DOM.

##### <template\>

Additionally, a [template](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template) can be utilized to insert markup. The provided `<template>` will be automatically instantiated and inserted into the Shadow DOM.
