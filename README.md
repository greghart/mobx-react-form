# MobX React Form

##### Automagically manage React forms state and automatic validation with MobX.

[![Travis Build](https://img.shields.io/travis/foxhound87/mobx-react-form/master.svg)](https://travis-ci.org/foxhound87/mobx-react-form)
[![Codecov Coverage](https://img.shields.io/codecov/c/github/foxhound87/mobx-react-form/master.svg)](https://codecov.io/gh/foxhound87/mobx-react-form)
[![npm](https://img.shields.io/npm/v/mobx-react-form.svg)]()
[![node](https://img.shields.io/node/v/mobx-react-form.svg)]()
[![GitHub license](https://img.shields.io/github/license/foxhound87/mobx-react-form.svg)]()
[![Downloads](https://img.shields.io/npm/dt/mobx-react-form.svg)]()
[![Downloads](https://img.shields.io/npm/dm/mobx-react-form.svg)]()

[![NPM](https://nodei.co/npm/mobx-react-form.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/mobx-react-form/)

---

## Features

- Automatic Reactive Form State Management with MobX Magic.
- Automatic Reactive Validation & Error Messages.
- Validation Plugins & Multiple Validation Styles.
- Nested Fields (w/ Serialization & Validation).
- Support for Sync & Async Validation functions (w/ Promises).
- Support for Material UI, React Widgets, React Select & more.
- Dedicated [DevTools](https://github.com/foxhound87/mobx-react-form-devtools) Package.

### TypeScript Support

A [TypeScript Branch](https://github.com/foxhound87/mobx-react-form/tree/typescript/) has been created. Feel free to contribute!

<br>

## Documentation

[https://foxhound87.github.io/mobx-react-form](https://foxhound87.github.io/mobx-react-form)

## Live Demo

[https://foxhound87.github.io/mobx-react-form/demo.html](https://foxhound87.github.io/mobx-react-form/demo.html)

## Demo Code

[https://github.com/foxhound87/mobx-react-form-demo](https://github.com/foxhound87/mobx-react-form-demo)

## Tutorial
[Automagically manage React forms state and automatic validation with MobX](https://medium.com/@foxhound87/automagically-manage-react-forms-state-with-mobx-and-automatic-validation-2b00a32b9769)


<br>

## Quick Start

```bash
npm install --save mobx-react-form
```

#### Choose and Setup a Validation Plugin

> See [Validation Plugins & Modes](https://foxhound87.github.io/mobx-react-form/docs/validation/plugins.html)
 and [Supported Validation Packages](https://foxhound87.github.io/mobx-react-form/docs/validation/supported-packages.html) for more info.

Below we are creating a `plugins` object using the `validatorjs` package to enable `DVR` functionalities (Declarative Validation Rules).

```javascript
import validatorjs from 'validatorjs';

const plugins = { dvr: validatorjs };
```

#### Define the Form Fields

Define the `fields` as a collection with a `rules` property for the validation.

```javascript
const fields = [{
  name: 'email',
  label: 'Email',
  placeholder: 'Insert Email',
  rules: 'required|email|string|between:5,25',
}, {
  name: 'password',
  label: 'Password',
  placeholder: 'Insert Password',
  rules: 'required|string|between:5,25',
}, {
  name: 'passwordConfirm',
  label: 'Password Confirmation',
  placeholder: 'Confirm Password',
  rules: 'same:password',
}];
```

> You can also define `fields` as an `object`.

#### Define the Validation Handlers

```javascript
import MobxReactForm from 'mobx-react-form';

class MyForm extends MobxReactForm {

  onSuccess(form) {
    alert('Form is valid! Send the request here.');
    // get field values
    console.log('Form Values!', form.values());
  }

  onError(form) {
    // get all form errors
    console.log('All form errors', form.errors());
    // invalidate the form with a custom error message
    form.invalidate('This is a generic error message!');
  }
}
```

> The Validation Handlers can be decoupled from the class as well.

#### Initialize the Form

Simply pass the `fields` and `plugins` objects to the constructor

```javascript
export default new MyForm({ fields, plugins });
```

#### Pass the form to a react component

The package provide some built-in and ready to use Event Handlers:

`onSubmit(e)`, `onClear(e)`, `onReset(e)` & [more...](https://foxhound87.github.io/mobx-react-form/docs/events/events-handlers.html)

```javascript
import React from 'react';
import { observer } from 'mobx-react';

export default observer(({ form, events }) => (
  <form onSubmit={form.onSubmit}>
    <label htmlFor={form.$('username').id}>
      {form.$('username').label}
    </label>
    <input type="text"
      id={form.$('username').id}
      name={form.$('username').name}
      value={form.$('username').value}
      placeholder={form.$('username').placeholder}
      onChange={form.$('username').onChange}
    />
    <p>{form.$('username').error}</p>

    ...

    <button type="submit" onClick={form.onSubmit}>Submit</button>
    <button type="button" onClick={form.onClear}>Clear</button>
    <button type="button" onClick={form.onReset}>Reset</button>

    <p>{form.error}</p>
  </form>
));
```

> Other Field Props are available. See the [docs](https://foxhound87.github.io/mobx-react-form/docs/api-reference/fields-properties.html) for more details.

<br>

## Contributing

If you want to contribute to the development, do not hesitate to fork the repo and send pull requests.

And don't forget to star the repo, I will ensure more frequent updates! Thanks!

