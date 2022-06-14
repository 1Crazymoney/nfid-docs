---
title: Basic installation
position: 3
category: Get Started
description: "The complete guide to NFID: the easy to implement, decentralized one-touch MFA and authorization platform."
---

## Requirements for Internet Computer applications
This guide assumes familiarity with building on the IC. More information can be found [here](https://internetcomputer.org/docs/current/developer-docs/build/install-upgrade-remove). Your environment will need:
- dfx SDK
- node
- @dfinity/agent, @dfinity/identity, and @dfinity/auth-client node packages >v0.11.0

## The authentication client
For a basic typescript integration inclusive of how to make authenticated calls locally in your development environment, follow along with our fork of Kyle Peacock's repository [here for typescript](https://github.com/internet-identity-labs/nfid-auth-client-demo/tree/feature/nfid-auth-client-demo) and [here](https://github.com/internet-identity-labs/nfid-auth-client-demo/tree/vanilla-js) for vanilla javascript.

## Replacing existing identity provider
If you already have Internet Identity authentication set up and want to switch to NFID, simply change the existing `identityProvider` URL in your `authClient.login({})` and customize with your application's name and logo:
```js
  // Your application's name (URI encoded)
  const APPLICATION_NAME = "Your%20Application%20Name";

  // URL to 37x37px logo of your application (URI encoded)
  const APPLICATION_LOGO_URL = "https%3A%2F%2Flogo.clearbit.com%2Fclearbit.com";

  const AUTH_PATH = "/authenticate/?applicationName="+APPLICATION_NAME+"&applicationLogo="+APPLICATION_LOGO_URL+"#authorize";

  // Replace https://identity.ic0.app with NFID_AUTH_URL
  // as the identityProvider for authClient.login({}) 
  const NFID_AUTH_URL = "https://nfid.one" + AUTH_PATH;
``` 

## Open auth in new window instead of new tab
We've added an option to open authentication windows in a new window instead of the default new tab opener. Just pass the variable `windowOpenerFeatures` with html options (like these default options we recommend passing) in your `authClient.login({})`:

```js
windowOpenerFeatures: 
  `left=${window.screen.width / 2 - 200}, `+
  `top=${window.screen.height / 2 - 300},` +
  `toolbar=0,location=0,menubar=0,width=400,height=600`
```

<img src="account_selection_screen.png" style="width:200px;margin:auto;"></img>

## Migrating existing users
If you have existing users, their user profile type will need a has_many relationship to principals instead of a has_one.

We are working on a frontend plugin that packages a UX for your users to authenticate with both the original identity provider and NFID, as well as the rust & motoko examples for how a user_profile might migrate from a has_one to a has_many relationship with principals.

If you'd like to get started sooner, just know that this is the process and it is entirely separate from NFID.