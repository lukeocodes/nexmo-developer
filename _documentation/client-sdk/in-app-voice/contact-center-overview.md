---
title: Contact Center Use Case
products: 
    - client-sdk
    - conversation
    - voice/voice-api
description: How to build your own contact center application.
navigation_weight: 4
---

# Build Your Own Contact Center

## Overview

In these guides, you’ll learn how to build an application with contact center features.

Your contact center application has 2 agents: `Jane` and `Joe`, that use your app. The caller will use a phone, to call into the call center.

- A client app, for your contact center agents. They can make and receive calls, and much more. You’ll use [Nexmo Client SDK](/client-sdk/in-app-voice/overview) to create that app.

- A server-side application. To use the SDK you must have a backend application. Some methods, like managing users can only be done through the backend. Other things (like creating conversations for example) can be done by both client and server side. You’ll do that with [Conversation API.](/conversation/overview)

- For more advanced voice functionality, you’ll utilize Nexmo [Voice API](/voice/voice-api/overview) on your backend side application.

> **NOTE:** Under the hood, Nexmo Voice API uses Conversation API as well and allows you to use conversations for Voice capabilities in a smoother fashion. That means that all communication is done over a [Conversation](/conversation/conversation), that allows you to maintain the communication context over time, for any communication channel you will choose.

## Before You Begin

Make sure you have a Nexmo account. If you don't yet [sign up](https://dashboard.nexmo.com/) for free to get started!

Take a note of your *api key* and *api secret*.

## Set Up Your Backend

### 1. Choose Your Backend

Deploy one of our sample backend application, in your prefered language. They are all on available on GitHub so you can explore the code and deploy it yourself.

<div class="Vlt-grid">
	<div class="Vlt-col">
        <a class="Vlt-card Vlt-card--clickable" target="_blank" href="https://github.com/nexmo-community/contact-center-rails">
            <div class="Vlt-card__image" style="height: 120px; background-image: url('/assets/images/brands/rails.png'); background-size: cover; background-position: center"></div>
            <div class="Vlt-card__content">
                <h4>Ruby on Rails</h4>
                Set up the Ruby on Rails backend.
            </div>
        </a>
	</div>
	<div class="Vlt-col">
        <a class="Vlt-card Vlt-card--clickable" target="_blank" href="https://github.com/nexmo-community/client-sdk-server-express">
            <div class="Vlt-card__image" style="height: 120px; background-image: url('/assets/images/brands/express.png'); background-size: cover; background-position: center"></div>
            <div class="Vlt-card__content">
                <h4>Express.js</h4>
                Set up the Express backend.
            </div>
        </a>
	</div>
	<div class="Vlt-col">
        <a class="Vlt-card Vlt-card--clickable" target="_blank" href="https://github.com/nexmo/client-sdk-server-kotlin">
            <div class="Vlt-card__image" style="height: 120px; background-image: url('/assets/images/brands/kotlin.png'); background-size: cover; background-position: center"></div>
            <div class="Vlt-card__content">
                <h4>Kotlin</h4>
                Set up the Kotlin backend.
            </div>
        </a>
	</div>
</div>

#### -or-

Integrate to your own backend application. Follow along and use the API directly to gain the same functionality.

### 2. Create Nexmo Application

Once you have created a Nexmo Account you will be able to create multiple [Nexmo Applications](/conversation/concepts/application). A Nexmo Application can contain a unique set of [Users](/conversation/concepts/user) and [Conversations](/conversation/concepts/conversation).

- If you deployed one of our demo backend applications on the previous step, you will need to:
  -  login in using your *api key* and *api secret*
    ![Login](/assets/images/client-sdk/contact-center/login.png)
  - and then you can create a new application by entering a name and clicking *Create*:
    ![Setup](/assets/images/client-sdk/contact-center/setup.png)

- Otherwise, you can also use the [API directly](/concepts/guides/applications/curl#getting-started-with-applications)

### 3. Connect a Nexmo Number

In order to make and receive calls, you should have a [Nexmo Number](/numbers/overview) connected to your Nexmo application.

To set that up, you can either assign a number you already own or buy a new number.

The demo backend application will give you basic features to start with. For more details and number management, check out the [Numbers API](/numbers/overview) or visit the [dashboard](https://dashboard.nexmo.com/buy-numbers).

#### 3.1. Buy a new Nexmo Number

If you already have a Nexmo number that you had bought and want to use, you don't have to buy a new number.

To buy a new number for your application, navigate to the **Numbers** tab and select the country to search numbers in.

![Number search](/assets/images/client-sdk/contact-center/numbers-search.png)

After you bought the number you can assign it to your application.

#### 3.2. Assign a Nexmo Number

To assign a number you already own, navigate to the **Numbers** tab and select the number to assign:

![Number assign](/assets/images/client-sdk/contact-center/numbers.png).

### 4. Create Users

A [user](/conversation/concepts/user) can log in to your application, in order to use the Nexmo Client and Conversation API functionality, such as create a conversation, join a conversation, and more.

To create users:

- If you are using the demo application, on the top menu select **Users** and then **New User**.

![New User](/assets/images/client-sdk/contact-center/users-new.png)

- Otherwise you can use the [Conversation API directly](https://developer.nexmo.com/api/conversation#createUser).

For the purpose of this guide, you should create two users, that will represent two agent on your contact center application. Create a user with the name `Jane` and another user with the name `Joe`.

![New User](/assets/images/client-sdk/contact-center/users.png)

### 5. Authenticate Users

The Nexmo Client SDKs use [JWTs](https://jwt.io/) for authentication when a user logs in. These JWTs are generated using the application ID and private key that is provided when a new application is created.

For security reasons, your client should not hold your private key. Therefore, the JWT must be provided by your backend.

Your backend should expose an endpoint that would allow the client to ask for a valid JWT per user. In a real life scenario, you would probably add some further authentication method such as a password. For this use case, sending your username will do.

- If you are using the demo backend application, it exposes a simple endpoint for that case. Click **SDK Integration** on the top menu. Under **User Authorization** you will find the exposed endpoint, the request and response bodies.

![SDK integration](/assets/images/client-sdk/contact-center/sdk-integration.png)

- Otherwise, you can use [Nexmo Server Libraries](/conversation/concepts/jwt-acl#nexmo-client-libraries) or other method of your choice.

You may update your JWT and adjust the user's permissions, the expiration date and more. Read more about JWT and ACL [in this topic](/conversation/concepts/jwt-acl).


## Set Up Your Client

Nexmo Client SDK is currently supported in Javascript, iOS and Android.

### 1. Choose Your Client

<div class="Vlt-grid">
	<div class="Vlt-col">
        <a class="Vlt-card Vlt-card--clickable" target="_blank" href="https://github.com/nexmo-community/contact-center-react">
            <div class="Vlt-card__image" style="height: 120px; background-image: url('/assets/images/brands/rails.png'); background-size: cover; background-position: center"></div>
            <div class="Vlt-card__content">
                <h4>React</h4>
                Set up the React client.
            </div>
        </a>
	</div>
	<div class="Vlt-col">
        <a class="Vlt-card Vlt-card--clickable" target="_blank" href="https://github.com/nexmo-community/contact-center-swift">
            <div class="Vlt-card__image" style="height: 120px; background-image: url('/assets/images/brands/express.png'); background-size: cover; background-position: center"></div>
            <div class="Vlt-card__content">
                <h4>Swift</h4>
                Set up the Swift iOS client.
            </div>
        </a>
	</div>
	<div class="Vlt-col">
        <a class="Vlt-card Vlt-card--clickable" target="_blank" href="https://github.com/nexmo-community/contact-center-objective-c">
            <div class="Vlt-card__image" style="height: 120px; background-image: url('/assets/images/brands/kotlin.png'); background-size: cover; background-position: center"></div>
            <div class="Vlt-card__content">
                <h4>Objective-C</h4>
                Set up the Objective-C iOS backend.
            </div>
        </a>
	</div>
	<div class="Vlt-col">
        <a class="Vlt-card Vlt-card--clickable" target="_blank" href="#tbc">
            <div class="Vlt-card__image" style="height: 120px; background-image: url('/assets/images/brands/kotlin.png'); background-size: cover; background-position: center"></div>
            <div class="Vlt-card__content">
                <h4>Kotlin/Java</h4>
                Set up the Kotlin/Java Android client.
            </div>
        </a>
	</div>
</div>

#### -or-

### 2. Integrate the SDK to your own client

Integrate the SDK to your own client side application:
    1. [Add the SDK to your existing app](/client-sdk/setup/add-sdk-to-your-app)
    2. [Add in-app voice functionality](/client-sdk/in-app-voice/guides/start-and-receive-calls)
    3. Create a simple API client to consume the JWT endpoint shown above.

At this point you have a client side application and a backend application to support it.

You can run the client app on two different devices, and log in as the user `Jane` on one device and the user `Joe` on the other.

You are now ready to make and receive calls, and add other advanced voice functionality with Nexmo Voice API.

## Add Voice Functionality

For each Nexmo Application, you can define an `answer_url`. That is a [webhook](/concepts/guides/webhooks) which Nexmo makes a request to as soon as your Nexmo number is being called to.
The `answer_url` contains the actions that will execute throughout the call. It does that by defining those actions in a JSON it returns, which follows the [Nexmo Call Control Object (NCCO)](/voice/voice-api/ncco-reference).

Updating the NCCO that returns from your `answer_url` changes the call functionality and allows you to add rich capabilities to your contact center application. To do this, navigate to the **App Settings** tab and click on **Edit NCCO**:

[screeshot to be added]

### Receive calls

For the basic use case, when a caller calls the contact center application, create a conversation and direct it to the agent Jane. 

The following NCCO, connects the called to user Jane:

```json
[
    {
        "action": "talk",
        "text": "Thank you for calling Jane"
    },
    {
        "action": "connect",
        "endpoint": [
            {
                "type": "app",
                "user": "jane"
            }
        ]
    }
]
```

To try it out, call the number assigned to your app.

### Make calls

This is how to allow the Jane to call from the app to a phone number (please make sure you are using your Nexmo number as required):

```json
[
    {
        "action": "talk",
        "text": "Please wait while we connect you."
    },
    {
        "action": "connect",
        "timeout": 20,
        "from": "YOUR_NEXMO_NUMBER",
        "endpoint": [
            {
                "type": "phone",
                "number": "CALLEE_PHONE_NUMBER"
            }
        ]
    }
]
```

To try it out, tap the "Call" button in the client app. 

### Create an IVR

When the caller calls the contact center, they hear "Thank you for calling my contact center. To talk to Jane please press 1, or to talk to Joe press 2."

```json
[
    {
        "action": "talk",
        "text": "Thank you for calling my contact center.",
        "voiceName": "Amy",
        "bargeIn": false
    },
    {
        "action": "talk",
        "text": "To talk to Jane, please press 1, or, to talk to Joe, press 2.",
        "voiceName": "Amy",
        "bargeIn": true
    },
    {
        "action": "input",
        "eventUrl": ["YOUR_SERVER_URL/webhooks/dtmf"]
    }
]
```

The input is processed by a specialised webhook - please make sure you are using your server URL above.

Try it out by calling the number associated with the app.

### Call Queue
User call an agent → stream music → connect to agent (according to backend trigger)

try it out.

### Call Whisper
Jane whispers to Joe

try it out.

### Hot Transfer
agent presses a button to transfer the call.

try it out.


## Wrap Up

Congratulations! you have created your contact center application!

You have:

- a client side application, that uses NexmoClient SDK
- a backend application to enable user management, authorization, defining an NCCO and more.
- an NCCO that defines the rich voice experience

### What's Next?
- [Add push notification to your mobile app](/client-sdk/setup/set-up-push-notifications)
- Explore [Client SDK](/client-sdk/overview)
- Explore [Voice API](/conversation/overview)
- Explore [Conversation API](/conversation/overview)
