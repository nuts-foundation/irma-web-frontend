# IRMA web front-end

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

## Technical design considerations

We want to make embedding an IRMA disclosure flow in your website as simple as
we can. We'll start with the required design elements that cover the different
states of the flow, so we can connect those to the `irmajs` javascript
implementation. We may later add a small javascript abstraction and add a
dependency on `irmajs`, to make things even simpler.

## UX considerations

Essentially we're guiding the user through a state machine, where for each state
we help the user recognise the next step to take. We visually mirror the design
of the IRMA app to help users make the subconscious connection between the
website and the app.

### The state machine

The state machine knows these states:

 1. Uninitialised
 2. Loading
 3. Showing QR code
 4. Code scanned, continue on phone
 5. Disclosure cancelled
 6. Disclosure timed out
 7. Disclosure errored
 8. Browser is not supported
 9. Success

The happy path for this flow is:

```
1. Uninitialised →
  2. Loading →
    3. Showing QR code →
      4. Code scanned, continue on phone →
        9. Success
```

States 5 - 8 are all basically just catching different edge-cases.

## Embedding in your application

This section is TODO. Sorry for that ;)

## Contributing

This section is largely TODO. Sorry for that ;)

Feel free to make pull requests on this repository. If you do, don't forget to
sign off your commits:

```bash
$ git commit --signoff
```
