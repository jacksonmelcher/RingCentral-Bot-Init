# RingCentral-bot-template [![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Dependency Status][daviddm-image]][daviddm-url] [![Coverage percentage][coveralls-image]][coveralls-url]

A template repo for making RingCentral Bots.

### Yeoman generator
I started working on a [Yeoman](https://yeoman.io/) Generator that can be found here: https://github.com/jacksonmelcher/generator-glip-bot

## Use template

Ensure you are **logged into your GitHub account** and click this [link](https://github.com/jacksonmelcher/ringcentral-bot-template/generate) or click `Use this Template`.

This chatbot is powered by the [ringcentral-chatbot framework for JavaScript](https://github.com/tylerlong/ringcentral-chatbot-js).

If you need help creating a bot follow these directions or visit [Tyler Long's Repo](https://github.com/tylerlong/glip-ping-chatbot/tree/express).

---

### Create bot and get credentials

[Create bot](https://developer.ringcentral.com/new-app?name=Sample+Bot+App&desc=A+sample+app+created+for+the+javascript+chatbot+framework&public=true&type=ServerBot&permissions=ReadAccounts,EditExtensions,SubscriptionWebhook,Glip&redirectUri=https://%3Cchatbot-server%3E/bot/oauth)

### Install dependencies

```
yarn install
```
### Upgrade dependencies

```
npx yarn-upgrade-all
```

### Start ngrok to get a public address

This step is optional if you have other ways to get your bot a public address. For example, you might have an VPS with public IP address. But ngrok is pretty handy during development phase:

```
yarn ngrok
```

Please take a note of the public address with scheme "https", it should be in the form of `https://xxxxx.ngrok.io`. We will need it soon.

Port 3000 is where we run our bot's Express.js process.

In content below, we call this public address `https://<chatbot-server>`.

### Specify environment variables:

Create `.env` files:

```
cp .express.env .env
```

- `RINGCENTRAL_SERVER`, use https://platform.dev.ringcentral.com for sandbox and https://platform.ringcentral.com for production
- `RINGCENTRAL_CHATBOT_DATABASE_CONNECTION_URI`, please sepcify connection URI to a relational database.
  - It is recommended to use SQLite for development: `sqlite://./db.sqlite`
- `RINGCENTRAL_CHATBOT_CLIENT_ID` & `RINGCENTRAL_CHATBOT_CLIENT_SECRET` could be found in the newly created RingCentral app.
- `RINGCENTRAL_CHATBOT_SERVER` is the public address generated by ngrok
  - For example, https://xxxxx.ngrok.io
  - For produciton, you might put your app behind nginx/apache and use the public address of those HTTP servers.
- `RINGCENTRAL_CHATBOT_EXPRESS_PORT` is the port we used for Express.js. It should match the ngrok command above.
- `RINGCENTRAL_CHATBOT_ADMIN_USERNAME` & `RINGCENTRAL_CHATBOT_ADMIN_PASSWORD` are the admin username and password.
  - Admin is the bot admin. It's normally the bot creator or maintainer.

### Create database tables

```
curl -X PUT -u admin:password https://<chatbot-server>/admin/setup-database
```

`admin` & `password` are defined in `.env` file we created above.

For more information, please read [setup database](https://github.com/tylerlong/ringcentral-chatbot-js#setup-database).

### Add the bot to Glip

Follow these steps to [add](https://github.com/tylerlong/glip-ping-chatbot/tree/master#add-the-bot-to-glip) the bot to Glip.


### Start Developing

```
yarn start:dev
```
