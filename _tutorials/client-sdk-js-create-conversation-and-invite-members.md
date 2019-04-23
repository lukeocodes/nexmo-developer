---
title: How to Create a Conversation with the Nexmo Client SDK in JavaScript
products: client-sdk
description: This tutorial shows you how to use the Nexmo Client SDK in your JavaScript application in order to create a conversation and invite members.
languages:
    - JavaScript
---

# How to Create a Conversation with the Nexmo Client SDK in JavaScript

```partial
source: _partials/client-sdk/message/conversation-intro.md
```

## Nexmo Concepts

```partial
source: _partials/client-sdk/message/conversation-concepts.md
```

## Prerequisites

```partial
source: _partials/client-sdk/message/conversation-prerequisites.md
```

## Adding the Nexmo Client to Your Application

Start with a blank HTML page and add a very basic UI for the conversation functionality. 

This contains:
- A simple login area. You will stub out a fake login process, but in a real application it would be expected for you to integrate with your chosen login system.
- A list of messages. All the messages will be output to this area.
- An input area. You will use this to send a new message.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    #login, #messages {
      width: 80%;
      height: 300px;
    }

    #messages {
      display: none;
    }
  </style>
</head>
<body>

  <form id="login">
    <h1>Login</h1>
    <input type="text" name="username" value="">
    <input type="submit" value="Login" />
  </form>

  <section id="messages">
    <h1>Messages</h1>

    <div id="messageFeed"></div>

    <textarea id="messageTextarea"></textarea>
    <br>
    <button id="send">Send</button>
  </section>

  <script>
    // Your code will go here
  </script>

</body>
</html>
```

We'll need to add the Nexmo Client to it, in order to do that we'll install it from NPM first, by running this command in the same folder as your `index.html` file:

```bash
$ npm install nexmo-client --save
```

## Login

```partial
source: _partials/client-sdk/message/javascript/login.md
```
