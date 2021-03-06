_Please note that this repository has been handed over to the Privacy by Design foundation. You can find the latest version here: https://github.com/privacybydesign/irma-frontend-packages_


# IRMA web front-end

![Screenshot of the IRMA component](screenshot.gif)

_See [the examples in the styleguide](https://nuts-foundation.github.io/irma-web-frontend/section-examples.html)
for more visual examples._

Implementing IRMA disclosure flows for verifying credentials or allowing users
to log in using IRMA can be a bit daunting, from a UX perspective. IRMA has a
lot of different states that the user has to be guided through and the whole
thing needs to be interactive.

Also, from a user's point of view, it will be beneficial to the adoption of IRMA
for these kinds of flows if they are easily recognisable and have similar
predictable behaviour. Seen one, seen them all.

For these reasons we have released this important part of the
[Helder application](https://helder.health) as a stand-alone open source package
that you can embed in your own (web based) applications.

This package has been designed and tested to work with the browsers Chrome,
Firefox, Safari, Opera, Edge and IE11.

## Technical design considerations

We want to make embedding an IRMA disclosure flow in your website as simple as
we can. This package only provides the required design elements that cover the
different states of the flow. If you want to make these designs actually work
with the IRMA app and the IRMA server, take a look at [`irma-web-glue`](https://github.com/nuts-foundation/irma-web-glue).

## UX considerations

Essentially we're guiding the user through a state machine, where for each state
we help the user recognise the next step to take. We visually mirror the design
of the IRMA app to help users make the subconscious connection between the
website and the app.

### The state machine

The state machine knows these states:

 1. Uninitialised
 2. Loading
 3. Transition to IRMA app
    * Showing QR code (desktop)
    * Showing IRMA button (mobile)
 4. Code scanned, continue on phone (desktop)
 5. Disclosure cancelled
 6. Disclosure timed out
 7. Disclosure errored
 8. Browser is not supported
 9. Success

The happy path for this flow is:

```
1. Uninitialised →
  2. Loading →
    3. Transition to IRMA app →
      (4. Code scanned, continue on phone) →
         9. Success
```

States 5 - 8 are all basically just catching different edge-cases.

## Embedding in your application

This project currently only contains CSS. So basically you just include the CSS
file(s) and find the right HTML snippets [in the styleguide](https://nuts-foundation.github.io/irma-web-frontend/section-examples.html).

### The old fashioned way

There is a normal version and a minified version of the styles [available for
download on Github](https://github.com/nuts-foundation/irma-web-frontend/tree/master/dist)
that you can include in your own project. If you don't even want to host the CSS
files yourself you can link from your project to the latest version like so:

```html
<link rel="stylesheet" href="//nuts-foundation.github.io/irma-web-frontend/application.css" />
```

Please be aware though that we can make breaking changes at any time.

### The way the cool kids do it

Alternatively, you can install it as an npm package. This can be useful if you
want to use (parts of) the SCSS behind it and override some variables, if you
need to package it in some complicated way or if you want to stay up to date.

```bash
$ npm install irma-web-frontend
```

You can then pull from the entire thing or just bits and pieces of it in your
SCSS/SASS:

```scss
  # The entire thing:
  @import "~irma-web-frontend/stylesheets";

  # Or just bits and pieces of it:
  @import "~irma-web-frontend/stylesheets/components/irma-form";
```

## Contributing

### Compiling locally

Requires a working `git` and `npm` on your machine.

```bash
# Clone the project
$ git clone git@github.com:nuts-foundation/irma-web-frontend.git

# Install dependencies
$ cd irma-web-frontend
$ npm install

# Run the compiler & dev server
$ npm run dev
```

You should now have the styleguide running on
[http://localhost:8080](http://localhost:8080).

Any change you make to the stylesheets will trigger a rebuild of the styleguide
and will be shown after a browser refresh.

### Making PRs

Please commit your changes in two steps for legibility:

```bash
# Commit your actual work:
$ git add stylesheets
$ git commit --signoff -m "Update button shadows to reflect new design"

# And then end with any updates to the living styleguide:
$ npm run clean # To make sure we're all good
$ git add docs
$ git commit --signoff -m "Rebuild the docs"
```

Then, feel free to make pull requests on this repository.

We sign off commits to indicate that we, as authors, are okay with releasing
this software under the license in the `LICENSE` file.
