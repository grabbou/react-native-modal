## react-native-modal

A `<Modal>` component for react-native. This is still very much a work
in progress and only handles the simplest of cases, ideas and
contributions are very welcome.

![Demo](https://raw.githubusercontent.com/brentvatne/react-native-modal/master/demo.gif)

## Add it to your project


1. Run `npm install react-native-modal --save`
2. Open your project in XCode, right click on `Libraries` and click `Add
   Files to "Your Project Name"` [(Screenshot)](http://url.brentvatne.ca/g9Wp).
3. Add `libRNModal.a` to `Build Phases -> Link Binary With Libraries`
   [(Screenshot)](http://url.brentvatne.ca/g9Wp).
3. `var Modal = require('react-native-modal');`
4. At the bottom of your app, add the `<Modal>` element and use its
   `isVisible` prop to toggle visibility. It needs to be at the bottom
   so that it appears above all other components when it is visible.
   If you use the `forceToFront` prop, then the position in the
   component tree does not matter at all - put it wherever you like.

## Usage

```javascript
'use strict';

var React = require('react-native');
var Modal = require('react-native-modal');
var { AppRegistry, StyleSheet, View, Text } = React;

class App extends React.Component {
  constructor() {
    this.state = {
      isModalOpen: false
    };
  }

  openModal() {
    this.setState({isModalOpen: true});
  }

  closeModal() {
    this.setState({isModalOpen: false});
  }

  render() {
    return (
      <View style={styles.page}>
        <Text onPress={() => this.openModal()}>
          Open Modal.
        </Text>
        <Modal isVisible={this.state.isModalOpen} onClose={() => this.closeModal()}>
          <Text>Hello world!</Text>
        </Modal>
      </View>
    );
  }
}

var styles = StyleSheet.create({
  page: {
    flex: 1,
    position: 'absolute',
    bottom: 0,
    left: 0,
    right: 0,
    top: 0
  }
});

AppRegistry.registerComponent('App', () => App);
```

If you would prefer to not have to implement `openModal()` and `closeModal()`, then you can use `Modal.Mixin`, then you can replace the definition of `App` above with:

```javascript
var App = React.createClass({
  mixins: [Modal.Mixin],

  render() {
    return (
      <View style={styles.page}>
        <Text onPress={() => this.openModal()}>
          Open Modal.
        </Text>
        <Modal backdropType="blur" isVisible={this.state.isModalOpen} onClose={() => this.closeModal()}>
          <Text>Hello world!</Text>
        </Modal>
      </View>
    );
  }
}
```

Also take a look on [react-native-login](https://github.com/brentvatne/react-native-login) for an example usage.

## Props

Component accepts several self-descriptive properties:

- **`forceToFront`** _(Bool)_ - if `true`, the modal will use a new `UIWindow` that will appear above `NavigatorIOS` and the status bar, but not alerts. [Demo of this here](https://raw.githubusercontent.com/brentvatne/react-native-modal/master/demo-layered.gif).
- **`hideCloseButton`** _(Bool)_
- **`backdropType`** _(String)_ `plain`, `none`, or `blur`. Default is `plain`.
- **`backdropBlur`** _(String)_ If `backdropType` is `blur`, this can be either `dark`, `light`, or `extra-light`. Default is `light`.
- **`isVisible`** _(Bool)_
- **`onClose`** _(Function)_
- **`onPressBackdrop`** _(Function)_ - callback to be fired when the user taps on the backdrop
- **`customCloseButton`** _(React Component)_
- **`customShowHandler`** _(Function)_ - uses [a react-tween-state wrapper](https://github.com/brentvatne/react-native-modal/blob/master/Transitions.js) API in order to show the modal. [See example](https://github.com/brentvatne/react-native-login/blob/master/App/Screens/LoginScreen.js#L84)
- **`customHideHandler`** _(Function)_ - uses [a react-tween-state wrapper](https://github.com/brentvatne/react-native-modal/blob/master/Transitions.js) API in order to hide the modal. [See example](https://github.com/brentvatne/react-native-login/blob/master/App/Screens/LoginScreen.js#L84)

---

**MIT Licensed**
