# React Native Fancy Alerts

[![NPM version][npm-image]][npm-url]
[![Downloads][downloads-image]][npm-url]
[![Twitter Follow][twitter-image]][twitter-url]

[npm-image]:http://img.shields.io/npm/v/react-native-expo-fancy-alerts.svg
[npm-url]:https://npmjs.org/package/react-native-expo-fancy-alerts
[downloads-image]:http://img.shields.io/npm/dm/react-native-expo-fancy-alerts.svg
[twitter-image]:https://img.shields.io/twitter/follow/xmr_nkr.svg?style=social&label=Follow%20me
[twitter-url]:https://twitter.com/xmr_nkr

## Inspired on [nativescript-fancyalert](https://github.com/NathanWalker/nativescript-fancyalert) - A simple, basic implementation of the beautiful alerts that lib brings to the table

### Intro

I used to be a Nativescript developer. One of the last libraries that I started using was [nativescript-fancyalert](https://github.com/NathanWalker/nativescript-fancyalert) and I really loved the extra touch of style it added to my interfaces.
As soon as I ran into the need for simple dialogs in my newest app which I'm developing with React Native I decided to go ahead and make something that looked like fancy alerts.

### The result will be something like this...

| ![Screenshot loading](screenshots/loading.png) | ![Screenshot success](screenshots/success.png) | ![Screenshot error](screenshots/error.png) |
| ---------------------------------------------- | ---------------------------------------------- | ------------------------------------------ |

### Quick Start

```javascript
import React, { Component } from "react";
import { View } from "react-native";
import { FancyAlert, LoadingIndicator } from "react-native-expo-fancy-alerts";

export default class MyComponent extends Component {
  state = {
    isLoading: false,
    errorMessage: {
      visible: false,
      message: ""
    }
  };

  startLoading = () => {
    if (!this.state.isLoading) {
      this.setState({ isLoading: true });
    }
  };

  finishLoading = () => {
    if (this.state.isLoading) {
      this.setState({ isLoading: false });
    }
  };

  showErrorAlert = message => {
    if (!this.state.errorAlert.visible) {
      this.setState({ errorAlert: { visible: true, message } });
    }
  };

  hideErrorAlert = () => {
    if (this.state.errorAlert.visible) {
      this.setState({ errorAlert: { visible: false, message: "" } });
    }
  };

  simulateLoading = () => {
    this.startLoading();

    setTimeout(() => {
      this.finishLoading();
    }, 300);
  };

  fakeError = () => {
    this.showErrorAlert("I failed... :(");
  };

  render = () => {
    const { isLoading, errorMessage } = this.state;

    return (
      <View>
        <TouchableOpacity onPress={this.simulateLoading}>
          <Text>Load now!!</Text>
        </TouchableOpacity>

        <TouchableOpacity onPress={this.fakeError}>
          <Text>Make me think I falied :(</Text>
        </TouchableOpacity>

        <LoadingIndicator visible={isLoading} />

        <FancyAlert
          visible={errorAlert.visible}
          icon={
            <Ionicons
              name={Platform.OS === "ios" ? "ios-close-outline" : "md-close"}
              size={36}
              color="#FFFFFF"
            />
          }
          customize={{
            accentColor: '#C3272B',
            backgroundColor: '#FFFFFF',
            contentTextStyle: {}, // optional
            btnTextStyle: {
              color: '#FFFFFF',
              marginLeft: 8
            }
          }}
          message={errorAlert.message}
          btnText="OK"
          onRequestClose={this.hideErrorAlert}
        />
      </View>
    );
  };
}
```

## Reference

### LoadingIndicator

| Property | Type | Required | Default | Description                                   |
| -------- | ---- | -------- | ------- | --------------------------------------------- |
| visible  | bool | yes      | n/a     | Whether the loading indicator should be shown |

### FancyAlert

| Property       | Type   | Required | Default    | Description                                            |
| -------------- | ------ | -------- | ---------- | ------------------------------------------------------ |
| visible        | bool   | yes      | n/a        | Whether the alert should be visible                    |
| icon           | node   | yes      | n/a        | The icon to show in the alert                          |
| customize      | object | yes      | n/a        | `{ accentColor: string, backgroundColor: string, contentTextStyle: StyleSheet, btnTextStyle: StyleSheet }` |
| message        | string | yes      | n/a        | The message to show the user                           |
| btnText        | string | yes      | n/a        | The text to put inside the button                      |
| onRequestClose | func   | no       | () => null | The action to run when the user taps the button        |

* NOTE -
  No dialog is closed by tapping the blurred background.

## Changelog

* 0.0.1 - Initial implementation - has layout issues on Android that WILL be fixed
* 0.0.2 - Android issue fixed
* 0.0.3 - Added extra customization options
* 1.0.0 - Years later I decided to package everything and release 🎉🥳
