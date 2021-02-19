---
name: 'JavaScript SDK'
---

## JavaScript SDK

You can use our Javascript SDK to interact with the bot as well as set event listeners for predetermined events, such as the start of a conversation.

### Setup

The Guide SDK is attached to the page's `window` object when the bot is initialized and is accessible via `window.GuideSDK` any time after that. Since Guide is injected asynchronously on the page, if you are defining event listeners on page load, it's highly unlikely the SDK will be initialized when your init script runs. To fix this, you can attach a function or an array of functions to `window.GuideSDKInit` and they will be executed when the SDK is initialized.

```html
<script>
  const onGuideSDKReady = () => {
    const logConversation = conversationId => console.log('conversationID', conversationId);

    window.GuideSDK.on('conversationStart', logConversation);

    window.GuideSDK.bot.setCustomSettings({ padding: 25 });
  };

  if (window.GuideSDK) {
    onGuideSDKReady();
  } else {
    window.GuideSDKInit = onGuideSDKReady; // this can also be an array of functions
  }
</script>
```

<hr>

### Event Listener

The Guide SDK offers an event listener that executes a callback when a predetermined event is fired. To attach an event listener, simply call:

```js
window.GuideSDK.on(eventName, callback);
```

To remove an event listener, you can call:

```js
window.GuideSDK.off(eventName, callback);
```

#### Events

| Event Name        | Payload                | Trigger                                                             | Example Payload                                        |
| ----------------- | ---------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------ |
| conversationStart | conversationId: String | New conversation is started (only occurs once per session) | `{ conversationId: '1afb23b2-8eb0-4972-8cdc-1cf59cffb540' }` |
| conversationEnd | `N/A` | Conversation is ended | |
| messageSend | message: String | Message sent through Guide | `{ message: 'Hello, World!' }` |
| messageReceive | author: String, message: String | Message received through Guide | `{ author: 'Scranton Healthcare', message: 'Hello, World!' }` |
| windowOpen | `N/A` | Guide UI window opened | |
| windowClose | `N/A` | Guide UI window closed | |

<hr>

### Bot API Reference

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
Initiate conversation with *message*.

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
  custom_first_name: 'Radric',
  custom_last_name: 'Davis',
  custom_account_number: '12345678',
  custom_birth_date: '07/07/1980',
  custom_phone_number: '770-999-0989',
  custom_email_address: 'radric@email.com',
  custom_address_1: '123 Main Street',
  custom_city: 'Atlanta',
  custom_state: 'GA',
  custom_zip: '30308',
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
  customClassName: 'bot-variant-a',
});
```

##### Description

Sets the bot's custom settings. This list is continuously growing, however we currently only offer two options.

| Key              | Type   | Example        | Description                                                                                              |
| :--------------- | :----- | -------------- | -------------------------------------------------------------------------------------------------------- |
| padding          | Int    | 25             | A number that will define the padding around the Guide launcher/ bot                                     |
| customClassName  | String | 'scranton-bot' | A value that will be added to the top level of the React component, allowing the client to run A/B tests |

##### Deprecated

You can also add these settings by setting them to the `window.guideSettings` object, however this is deprecated and may be removed from future versions.

```html
<-- add a script tag in your head to customize your Guide implementation -->
<script>
  window.guideSettings = {
    padding: 25,
    customClassName: 'scranton-bot',
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
