# launchdarkly
**CSE Demo of LaunchDarkly**

**Usage**

Go to https://harrisonkrat.github.io to test the `positive-message` feature flag. Depending on the name values entered, you will see one of two messages.
Change the name values entered and resubmit, or refresh the page and resubmit.
If you want to force both message values, submit:
1. First: Harrison, Last: Krat
2. First: 12345, Last: TestLast

**Code walkthrough**

The page utilizes the JavaScript SDK for a client-side implementation of LaunchDarkly.
Scripting renders the form, and the LD `user` is initialized upon page load.
The feature flag is not yet evaluated and the message is not yet rendered.
The form simulates a rudimentary login scenario. Upon submit:
1. the user object has its `firstName` and `lastName` values reset
2. `user.key` is reset as a base64-encoded string of `firstName` + space + `lastName`
3. a second function `pumpSunshine` is called

The `pumpSunshine` function calls `ldclient.identify()` to reinitialize the `user` JSON.
A 500ms timeout is set to give the SDK time to retrieve the feature flag values for the new user.
The form evaluates the feature flag and renders one of two messages depending on the returned value.
For each form submission without a page refresh, the message is replaced.

**Known limitations:**
1. The user's first and last name can be derived after submission by base64-decoding the `user.key` value.
2. The form is not cleared upon submission.
3. There is no CSS styling of the page.

**Feature flag**

Within my LaunchDarkly account, I set up one feature flag called `positive-message`.
 - It is a boolean flag.
 - The default value is `on`.
 - The default rule serves `true`.
 - If targeting is off, it serves `false`.
 - It has two targeting rules:
     1. If the user key's first character is in the regex range A-M, seerve `true`.
     2. If the user key's first character is in the regex range N-Z, seerve `false`.
 - The flag is available to SDKs using client-side `ID`.

**Resources used**
 - https://docs.launchdarkly.com/sdk/client-side/javascript
 - https://launchdarkly.github.io/js-client-sdk/interfaces/_launchdarkly_js_client_sdk_.ldclient.html
 - https://app.launchdarkly.com/default/production/quickstart
 - https://www.w3schools.com/
