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

| Event Name        | Payload                | Description                                                             | Example Payload                                        |
| ----------------- | ---------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------ |
| conversationStart | conversationId: String | Fired when a new conversation is started (only occurs once per session) | conversationId: '1afb23b2-8eb0-4972-8cdc-1cf59cffb540' |

<hr>

### Bot API

The Guide SDK also has an API that allows developers to interact with the bot directly via the `window.GuideSDK.bot` interface. These API calls can be invoked any time after the bot has been initialized.

#### setCustomVariables

##### Example

```js
window.GuideSDK.bot.setCustomVariables({
  custom_first_name: 'Radric',
  custom_last_name: 'Davis',
  custom_account_number: '12345678',
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

#### setCustomSettings

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
| disableShadowDOM | Bool   | true           | Disables the Shadow DOM wrapper. ⚠️Warning:⚠️ This could cause unintended style conflicts.               |

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
