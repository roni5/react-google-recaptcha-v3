# React Google Recaptcha V3

## Overview

`react-google-recaptcha-v3` is a library created to assist integrating Google ReCaptcha V3 to your React App.

## Install

```bash
npm install react-google-recaptcha-v3@next
```

## Usage

#### Provide Recaptcha Key

To use `react-google-recaptcha-v3`, you need to create a recaptcha key for your domain, you can get one from [here](https://www.google.com/recaptcha/intro/v3.html).

#### Components

##### GoogleReCaptchaProvider

`react-google-recaptcha-v3` provides a `GoogleReCaptchaProvider` provider component that should be used to wrap around your components.

`GoogleReCaptchaProvider`'s responsibility is to load the necessary reCaptcha script and provide access to reCaptcha to the rest of your application.

```javascript
import { GoogleReCaptchaProvider } from "react-google-recaptcha-v3";

ReactDom.render(
  <GoogleReCaptchaProvider reCaptchaKey="[Your recaptcha key]">
    <YourApp />
  </GoogleReCaptchaProvider>,
  document.getElementById("app")
);
```

Afterwards, there are three ways to trigger the recaptcha validation, the first is using the `GoogleReCaptcha` component. The second is using the HOC `withGoogleReCaptcha`, and the last approach is using the custom hook `useGoogleReCaptcha`.

#### GoogleReCaptcha

`GoogleRecaptcha` is a react component that can be used in your app to trigger the validation. It provides a prop `onVerify`, which will be called once the verify is done successfully.

```javascript
import {
  GoogleReCaptchaProvider,
  GoogleReCaptcha
} from "react-google-recaptcha-v3";

ReactDom.render(
  <GoogleReCaptchaProvider reCaptchaKey="[Your recaptcha key]">
    <GoogleReCaptcha onVerify={token => console.log(token)} />
  </GoogleReCaptchaProvider>,
  document.getElementById("app")
);
```

#### withGoogleReCaptcha

`GoogleRecaptcha` is a HOC (higher order component) that can be used to integrate reCaptcha validation with your component and trigger the validation programmatically. It inject the wrapped component with `googleReCaptchaProps` object.

The object contains the `executeRecaptcha` function that can be called to validate the user action.

```javascript
import {
  GoogleReCaptchaProvider,
  withGoogleReCaptcha
} from 'react-google-recaptcha-v3';

class ReCaptchaComponent extends React.Component {
  async componentDidMount() {
    const token = await this.props.googleReCaptchaProps.executeRecaptcha('homepage');
  }

  render() {
    ...
  }
}

const YourReCaptchaComponent = withGoogleReCaptcha(ReCaptchaComponent);

ReactDom.render(
  <GoogleReCaptchaProvider reCaptchaKey="[Your recaptcha key]">
    <YourReCaptchaComponent />
  </GoogleReCaptchaProvider>,
  document.getElementById('app')
);
```

#### React Hook: useGoogleReCaptcha

If you prefer a React Hook approach over the ol good Higher Order Component, you can choose to use the custom hook `useGoogleReCaptcha` over the HOC `withGoogleReCaptcha`.

It's very simple to use the hook:

```javascript
import {
  GoogleReCaptchaProvider,
  useGoogleReCaptcha
} from 'react-google-recaptcha-v3';

// Remember that the hook can only be used within a React functional component
const ReCaptchaComponent = () => {
  const { executeRecaptcha } = useGoogleReCaptcha();

  return (...)
}

ReactDom.render(
  <GoogleReCaptchaProvider reCaptchaKey="[Your recaptcha key]">
    <YourReCaptchaComponent />
  </GoogleReCaptchaProvider>,
  document.getElementById('app')
);
```

## Typescript

This project is written in typescript and fully support it.
