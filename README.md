# Node.js Twitch Helix Webhooks

[![Build Status](https://travis-ci.org/DaniilShev/node-twitch-webhook.svg?branch=master)](https://travis-ci.org/k-egor-smirnov/node-twitch-webhook)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)
[![dependencies Status](https://david-dm.org/DaniilShev/node-twitch-webhook/status.svg)](https://david-dm.org/k-egor-smirnov/node-twitch-webhook)
[![devDependencies Status](https://david-dm.org/DaniilShev/node-twitch-webhook/dev-status.svg)](https://david-dm.org/k-egor-smirnov/node-twitch-webhook?type=dev)
[![Node version](https://img.shields.io/node/v/twitch-webhook.svg?style=flat)](http://nodejs.org/download/)
[![https://nodei.co/npm/twitch-webhook.png?downloads=true&downloadRank=true&stars=true](https://nodei.co/npm/twitch-webhook.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/twitch-webhook)

## Installation

Install with NPM:

`npm install --save twitch-webhook`

## Usage

```
const TwitchWebhook = require('twitch-webhook');

const twitchWebhook = new TwitchWebhook({
    client_id: 'Your Twitch Client ID',
    callback: 'Your Callback URL'
    secret: 'It\'s a secret'
})

twitchWebhook.on('streams', ({ topic, event }) => {
    console.log(event);
})

twitchWebhook.on('users/follows', ({ topic, event }) => {
    console.log(event);
})

twitchWebhook.on('*', ({ topic, event }) => {
    console.log(event);
})

twitchWebhook.subscribe('users/follows', {
    from_id: 'User id'
})

twitchWebhook.subscribe('streams', {
    user_id: 'User id'
})
```

# Documentation

<a name="TwitchWebhook"></a>

## TwitchWebhook

TwitchWebHookAPI

**Kind**: global class

* [TwitchWebhook](#TwitchWebhook)
  * [new TwitchWebhook(options)](#new_TwitchWebhook_new)
  * [.errors](#TwitchWebhook+errors)
  * [.listen([...args])](#TwitchWebhook+listen) ⇒ <code>Promise</code>
  * [.close()](#TwitchWebhook+close) ⇒ <code>Promise</code>
  * [.isListening()](#TwitchWebhook+isListening) ⇒ <code>boolean</code>
  * [.subscribe(topic, options)](#TwitchWebhook+subscribe)
  * [.unsubscribe(topic)](#TwitchWebhook+unsubscribe)

<a name="new_TwitchWebhook_new"></a>

### new TwitchWebhook(options)

Constructs an instance of TwitchWebHookAPI

| Param                      | Type                                        | Default                                                | Description                                                                                |
| -------------------------- | ------------------------------------------- | ------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| options                    | <code>Object</code>                         |                                                        | Options                                                                                    |
| options.client_id          | <code>string</code>                         |                                                        | Client ID required for Twitch API calls                                                    |
| options.callback           | <code>string</code>                         |                                                        | URL where notifications will be delivered.                                                 |
| [options.secret]           | <code>string</code>                         |                                                        | Secret used to sign notification payloads.                                                 |
| [options.lease_seconds]    | <code>number</code>                         |                                                        | Number of seconds until the subscription expires.                                          |
| [options.listen]           | <code>boolean</code> \| <code>Object</code> |                                                        | Listen options                                                                             |
| [options.listen.autoStart] | <code>string</code>                         | <code>false</code>                                     | Should automaticaly starts listening                                                       |
| [options.listen.host]      | <code>string</code>                         | <code>&quot;0.0.0.0&quot;</code>         | Host to bind to                                                                            |
| [options.listen.port]      | <code>number</code>                         | <code>8443</code>                                      | Port to bind to                                                                            |
| [options.https]            | <code>boolean</code> \| <code>Object</code> | <code>false</code>                                     | Should use https connection. If yes, these options to be passed to `https.createServer()`. |
| [options.baseApiUrl]       | <code>string</code>                         | <code>&quot;https://api.twitch.tv/helix/\&quot;"</code> | Base Twitch API URL. It needs for proxying and testing                                     |

<a name="TwitchWebhook+errors"></a>

### TwitchWebhook.errors

Returns errors

**Kind**: instance property of [<code>TwitchWebhook</code>](#TwitchWebhook)
<a name="TwitchWebhook+listen"></a>

### TwitchWebhook.listen([...args]) ⇒ <code>Promise</code>

Start listening for connections

**Kind**: instance method of [<code>TwitchWebhook</code>](#TwitchWebhook)

| Param     | Type             | Description |
| --------- | ---------------- | ----------- |
| [...args] | <code>any</code> | Arguments   |

<a name="TwitchWebhook+close"></a>

### TwitchWebhook.close() ⇒ <code>Promise</code>

Stop listening for connections

**Kind**: instance method of [<code>TwitchWebhook</code>](#TwitchWebhook)
<a name="TwitchWebhook+isListening"></a>

### TwitchWebhook.isListening() ⇒ <code>boolean</code>

Checks if server is listening for connections.

**Kind**: instance method of [<code>TwitchWebhook</code>](#TwitchWebhook)
<a name="TwitchWebhook+subscribe"></a>

### TwitchWebhook.subscribe(topic, options)

Subscribes to specific topic

**Kind**: instance method of [<code>TwitchWebhook</code>](#TwitchWebhook)

| Param   | Type                | Description   |
| ------- | ------------------- | ------------- |
| topic   | <code>string</code> | Topic name    |
| options | <code>Object</code> | Topic options |

<a name="TwitchWebhook+unsubscribe"></a>

### TwitchWebhook.unsubscribe(topic)

Unsubscribes from specific topic

**Kind**: instance method of [<code>TwitchWebhook</code>](#TwitchWebhook)

| Param | Type                | Description |
| ----- | ------------------- | ----------- |
| topic | <code>string</code> | Topic name  |
