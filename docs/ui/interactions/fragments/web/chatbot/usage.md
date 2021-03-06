## Usage

<docs-filter framework="react">

```jsx
import React from "react";
import Amplify from "aws-amplify";
import {AmplifyChatbot} from "@aws-amplify/ui-react";
import awsconfig from "./aws-exports";

Amplify.configure(awsconfig);

const App = () => (
  <AmplifyChatbot
    botName="yourBotName"
    botTitle="My ChatBot"
    welcomeMessage="Hello, how can I help you?"
  />
);
```

</docs-filter>

<docs-filter framework="angular">

<inline-fragment src="~/ui/fragments/angular/configure-module.md"></inline-fragment>

_app.component.html_

```html
<amplify-chatbot
  bot-name="yourBotName"
  bot-title="My ChatBot"
  welcome-message="Hello, how can I help you?"
></amplify-chatbot>
```

</docs-filter>

<docs-filter framework="ionic">

<inline-fragment src="~/ui/fragments/angular/configure-module.md"></inline-fragment>

_app.component.html_

```html
<amplify-chatbot
  bot-name="yourBotName"
  bot-title="My ChatBot"
  welcome-message="Hello, how can I help you?"
></amplify-chatbot>
```

</docs-filter>

<docs-filter framework="vue">

<inline-fragment src="~/ui/fragments/vue/configure-app.md"></inline-fragment>

_App.vue_

```html
<template>
  <amplify-chatbot
    bot-name="yourBotName"
    bot-title="My ChatBot"
    welcome-message="Hello, how can I help you?"
  />
</template>
```

</docs-filter>

<ui-component-props tag="amplify-chatbot" prop-type="attr" use-table-headers></ui-component-props>

## Use Cases

### Setting Up Voice Chat

In order for voice input to work with Amazon Lex, you may have to enable output voice in [AWS Management Console](https://console.aws.amazon.com/console/home). Under the Amazon Lex service, click on your configured Lex chatbot and go to settings -> General and pick your desired output voice.

### Listening to Chat Fulfillment

Once a conversation session is finished, `amplify-chatbot` emits a custom event `chatCompleted` that your app can listen to:

<docs-filter framework="react">

```js
function App() {
  const handleChatComplete = (event) => {
    const {data, err} = event.detail;
    if (data) console.log("Chat fulfilled!", JSON.stringify(data));
    if (err) console.error("Chat failed:", err);
  };

  useEffect(() => {
    const chatbotElement = document.querySelector("amplify-chatbot");
    chatbotElement.addEventListener("chatCompleted", handleChatComplete);
    return function cleanup() {
      chatbotElement.removeEventListener("chatCompleted", handleChatComplete);
    };
  }, []);
}
```

</docs-filter>

<docs-filter framework="vue">

<amplify-block-switcher>
<amplify-block name="Vue 3">

```html
<script>
  const handleChatComplete = (event) => {
    const {data, err} = event.detail;
    if (data) alert("success!\n" + JSON.stringify(data));
    if (err) alert(err);
  };

  export default {
    name: "App",
    mounted() {
      const chatbotElement = this.$el.querySelector("amplify-chatbot");
      chatbotElement.addEventListener("chatCompleted", handleChatComplete);
    },
    beforeUnmount() {
      const chatbotElement = this.$el.querySelector("amplify-chatbot");
      chatbotElement.removeEventListener("chatCompleted", handleChatComplete);
    },
  };
</script>
```

</amplify-block>
<amplify-block name="Vue 2">

```html
<script>
  const handleChatComplete = (event) => {
    const {data, err} = event.detail;
    if (data) alert("success!\n" + JSON.stringify(data));
    if (err) alert(err);
  };

  export default {
    name: "App",
    mounted() {
      const chatbotElement = this.$el.querySelector("amplify-chatbot");
      chatbotElement.addEventListener("chatCompleted", handleChatComplete);
    },
    beforeDestroy() {
      const chatbotElement = this.$el.querySelector("amplify-chatbot");
      chatbotElement.removeEventListener("chatCompleted", handleChatComplete);
    },
  };
</script>
```

</amplify-block>

</docs-filter>

<docs-filter framework="angular">

```js
const handleChatComplete = (event: Event) => {
  const { data, err } = (event as any).detail;
  if (data) console.log('Chat fulfilled!', JSON.stringify(data));
  if (err) console.error('Chat failed:', err);
};

export class AppComponent implements OnInit, OnDestroy {
  ngOnInit(): void {
    const chatbotElement = document.querySelector('amplify-chatbot');
    chatbotElement.addEventListener('chatCompleted', handleChatComplete);
  }
  ngOnDestroy(): void {
    const chatbotElement = document.querySelector('amplify-chatbot');
    chatbotElement.removeEventListener('chatCompleted', handleChatComplete);
  }
}
```

</docs-filter>

<docs-filter framework="ionic">

```js
const handleChatComplete = (event: Event) => {
  const { data, err } = (event as any).detail;
  if (data) console.log('Chat fulfilled!', JSON.stringify(data));
  if (err) console.error('Chat failed:', err);
};

export class AppComponent implements OnInit, OnDestroy {
  ngOnInit(): void {
    const chatbotElement = document.querySelector('amplify-chatbot');
    chatbotElement.addEventListener('chatCompleted', handleChatComplete);
  }
  ngOnDestroy(): void {
    const chatbotElement = document.querySelector('amplify-chatbot');
    chatbotElement.removeEventListener('chatCompleted', handleChatComplete);
  }
}
```

</docs-filter>
