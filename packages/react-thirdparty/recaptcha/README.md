<h1 align="center">React Google ReCaptcha V3</h1>
<div align="center">

Integrating Google ReCaptcha V3

</div>

## Usage

### Provide ReCaptcha Key

To use this integration, you need to create a recaptcha key for your domain, you can get one from [here](https://www.google.com/recaptcha/intro/v3.html).

### Components

#### GoogleReCaptchaProvider

This submobule provides a `GoogleReCaptchaProvider` provider component that should be used to wrap around your components.

`GoogleReCaptchaProvider`'s responsibility is to load the necessary reCaptcha script and provide access to reCaptcha to the rest of your application.

You can customize the injected `script` tag with the `scriptProps` prop. This prop allows you to add `async`, `defer`, `nonce` attributes to the script tag. You can also control whether the injected script will be added to the document body or head with `appendTo` attribute. Example can be found belows. The `scriptProps` and its attributes are all optional.

It also provides an optional prop `language` to support different languages that is supported by Google ReCaptcha.

<https://developers.google.com/recaptcha/docs/language>

The provider also provide the prop `useReCaptchaNet` to load script from `recaptcha.net`:
<https://developers.google.com/recaptcha/docs/faq#can-i-use-recaptcha-globally>

```jsx
import { GoogleReCaptchaProvider } from '@nancy/react-thirdparty'

ReactDom.render(
  <GoogleReCaptchaProvider
    reCaptchaKey="[Your recaptcha key]"
    language="[optional_language]"
    useReCaptchaNet="[optional_boolean_value]"
    scriptProps={{
      async: false, // optional, default to false,
      defer: false // optional, default to false
      appendTo: "head" // optional, default to "head", can be "head" or "body",
      nonce: undefined // optional, default undefined
    }}
  >
    <YourApp />
  </GoogleReCaptchaProvider>,
  document.getElementById('app')
)
```

There are three ways to trigger the recaptcha validation: using the `GoogleReCaptcha` component or using the custom hook `useGoogleReCaptcha`.

### GoogleReCaptcha

`GoogleReCaptcha` is a react component that can be used in your app to trigger the validation. It provides a prop `onVerify`, which will be called once the verify is done successfully.

```jsx
import {
  GoogleReCaptchaProvider,
  GoogleReCaptcha,
} from "@nancy/react-thirdparty";

ReactDom.render(
  <GoogleReCaptchaProvider reCaptchaKey="[Your recaptcha key]">
    <GoogleReCaptcha onVerify={handleVerify} />
  </GoogleReCaptchaProvider>,
  document.getElementById("app")
);
```

```jsx
// IMPORTANT NOTES: The `GoogleReCaptcha` component is a wrapper around `useGoogleReCaptcha` hook and use `useEffect` to run the verification.
// It's important that you understand how React hooks work to use it properly.
// Avoid using inline function for the `onVerify` props as it can possibly cause the verify function to run continously.
// To avoid that problem, you can use a memoized function provided by `React.useCallback` or a class method
// The code below is an example that inline function can result in an infinite loop and the verify function runs continously:

const MyComponent: FC = () => {
  const [token, setToken] = useState();

  return (
    <div>
      <GoogleReCaptcha
        onVerify={(token) => {
          setToken(token);
        }}
      />
    </div>
  );
};
```

### React Hook: useGoogleReCaptcha

If you prefer a React Hook approach over the old good Component, you can choose to use the custom hook `useGoogleReCaptcha`.

It's very simple to use the hook:

```jsx
import {
  GoogleReCaptchaProvider,
  useGoogleReCaptcha
} from '@nancy/react-thirdparty'

const YourReCaptchaComponent  = () => {
  // you should use `useCallback` just when needed
  const handleVerify = useCallback((token) => {
    console.log(`Yay! token: ${token}`)
  }, [])

  useGoogleReCaptcha({
    action: "login_page",
    onVerify: handleVerify,
  })

  return (...)
}

ReactDom.render(
  <GoogleReCaptchaProvider reCaptchaKey="[Your recaptcha key]">
    <YourReCaptchaComponent />
  </GoogleReCaptchaProvider>,
  document.getElementById('app')
)
```
