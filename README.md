# Chabok Push Client for Javascript
This Chabok Push client library supports web browsers, web workers.

## Getting started



#### Yarn (or NPM)

You can use any NPM-compatible package manager, including NPM itself and Yarn.

```bash
npm install chabokpush --save
```
Or:
```bash
yarn add chabokpush
```

Then:

```javascript
import chabokpush from 'chabokpush';
```

Or, if you're not using ES6 modules:

```javascript
const chabokpush = require('chabokpush');
```
#### CDN

```html
<script src="https://unpkg.com/chabokpush@[X.Y.Z]/dist/chabokpush.min.js"></script>
```
Replace [X.Y.Z] with the latest version

## Initialization

```js
const auth = {
  appId: 'APP_ID',
  apiKey: 'API_KEY',
  username: 'USERNAME',
  password: 'PASSWORD',
  devMode:true
}
const options={silent: true}

const chabok = new chabokpush.Chabok(auth, options)
```
if devMode enabled you can Test your Project on development Mode.
You can get your `APP_ID`, `API_KEY`, `USERNAME` and `PASSWORD` from the [Chabok dashboard](http://sandbox.push.adpdigital.com/front/account/edit).

## Options

There are a number of configuration parameters which can be set for the ChabokPush client, which can be passed as an object to the ChabokPush constructor, i.e.:

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [options] | <code>Object</code> |  |  |
| [options.webpush] | <code>Object</code> |  |  |
| [options.webpush.enabled] | <code>Boolean</code> | <code>false</code> | Set true to enable push Notification |
| [options.silent] | <code>Boolean</code> | <code>true</code> | Receive messages Silently |


## Sample Usage

```js
const auth = {
  appId: 'APP_ID',
  apiKey: 'API_KEY',
  username: 'USERNAME',
  password: 'PASSWORD',
  devMode: true
}
const options={}

const chabok = new chabokpush.Chabok(auth, options)

chabok.on('registered', deviceId => console.log('DeviceId ', deviceId))

chabok.on('connected', _ => {
  console.log('Connected')
  chabok.enableDeliveryForEvent('geo')
})

chabok.on('message', msg => console.log('Message ', msg))
chabok.on('geo', geoEvent => console.log('Geo Event ', geoEvent))

chabok.on('connecting', _ => console.log('Reconnecting'))
chabok.on('disconnected', _ => console.log('offline'))
chabok.on('closed', _ => console.log('disconnected'))

chabok.register('012345678910111213')
```
