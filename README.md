# Indium mobile wallet

![Download Count](https://img.shields.io/github/downloads/IndiumCrypto/indium-mobile-wallet/total.svg)
![Open Issue Count](https://img.shields.io/github/issues/IndiumCrypto/indium-mobile-wallet)
![License](https://img.shields.io/github/license/IndiumCrypto/indium-mobile-wallet)
![Version](https://img.shields.io/github/v/release/IndiumCrypto/indium-mobile-wallet)

### Initial Setup

* `cd indium-mobile-wallet`
* `yarn install`

### Running

* `node --max-old-space-size=8192 node_modules/react-native/local-cli/cli.js start` (Just need to run this once to start the server, leave it running)
* `react-native run-android`

### Logging

`react-native log-android`

### Creating a release

You need to bump the version number in:

* `src/Config.js` - `appVersion`
* `android/app/build.gradle` - `versionCode` and `versionName`
* `package.json` - `version` - Not strictly required
* Update user agent in `android/app/src/main/java/com/indium/MainApplication.java` and `android/app/src/main/java/com/indium/TurtleCoinModule.java`

Then
`cd android`
`./gradlew bundleRelease`
Optionally
`./gradlew installRelease`

or `yarn deploy-android`

### Integrating QR Codes or URIs

Indiu supports two kinds of QR codes.

* Standard addresses / integrated addresses - This is simply the address encoded as a QR code.

* indium:// URI encoded as a QR code.

Your uri must begin with `indium://` followed by the address to send to, for example, `indium://<WALLET_ADDRESS>`

There are a few optional parameters.

* `name` - This is used to add you to the users address book, and identify you on the 'Confirm' screen. A name can contain spaces, and should be URI encoded.
* `amount` - This is the amount to send you. This should be specified in atomic units.
* `paymentid` - If not using integrated address, you can specify a payment ID. Specifying an integrated address and a payment ID is illegal.

An example of a URI containing all of the above parameters:

```
indium://<WALLET_ADDRESS>?amount=100000000&name=Starbucks%20Coffee&paymentid=<PAYMENT_ID>
```

This would send `1 IND` (100000000 in atomic units) to the address `<WALLETA_ADDRESS>`, using the name `Starbucks Coffee` (Note the URI encoding), and using a payment ID of `<PAYMENT_ID>`

You can also just display the URI as a hyperlink. If a user clicks the link, it will open the app, and jump to the confirm screen, just as a QR code would function. (Provided all the fields are given)
