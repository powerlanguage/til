## Same Origin

Two windows are said to have the **same origin** if they have the same **protocol**, **domain** and **port**.

Same origin:

- `http://site.com`
- `http://site.com/`
- `http://site.com/my/page.html`

Different origin:

- `http://www.site.com` (a different domain, `www`)
- `http://site.org` (a different domain, `org`)
- `https://site.com` (a different protocol, `https`)
- `http://site.com:8080` (a different port, `8080`)

The **same origin** policy dictates that:

- If we have a reference to another window and that window comes from the same origin, we have full access to that window.
- If the window comes from another origin, we cannot access the content of the window. Writing `location` is an exception, as it allows redirects.
- You can still access the window object itself

## Iframes

- You can access the window of an embedded iframe with `iframe.contentWindow`.
- You can access the content within the window of an embedded iframe with `iframe.contentDocument` (need to be on the **same origin**)

## Subdomains

Having a different subdomain means that two domains have different origins.

- `http://window1.site.com`
- `http://window2.site.com`

These are not part considered the **same origin** as they have different domains. However, because they share the same second level domain (`site.com`) we can make the browser ignore that difference so they can be considered **same origin** for cross-window communication by having each window run:

`document.domain = 'site.com'`

## postMessage

The `postMessage` interface allows windows to talk to each other no matter which origin they are from. This effectively gets around the **same origin** restriction.

We send a message by calling the `postMessage` method of the receiving/target window. E.g.

`targetWindow.postMessage(data, targetOrigin)`

- `data` should be a string
- `targetOrigin` specifies the origin for the target window

Because `targetWindow` may not be the **same origin** we may not be able to read its location and tell what origin it is. `targetOrigin` allows the sender to specify that the recipient must be on a specific origin.

To receive a message, the target window should add an event listener:

```
window.addEventListener("message", function(event) {
  event.data // the data
  event.origin // the origin of the sending window
  event.source // the window that sent the message

  if(event.origin !== 'http://site.com') {
      // unknown domain, abort
      return;
  }
  console.log(event.data);
  // send a message back to the sending window
  event.source.postMessage('message received', event.origin)
})
```

- https://javascript.info/cross-window-communication
