`document.cookie` returns a single string of cookie key/value pairs concatenated on `';'`.

> Note that each key and value may be surrounded by whitespace (space and tab characters): in fact, RFC 6265 mandates a single space after each semicolon, but some user agents may not abide by this.
> [source](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie)

To separate keys/values we have to indentify the first `'='` in the cookie string. We cannot use `cookieString.split('=')` as `'='` is a valid character for the cookie value to contain.

```
// Parses document.cookie into key/value object
function parseCookies() {
  return document.cookie.split(';').reduce((acc, item) => {
    const trimmedItem = item.trim();
    const splitIndex = trimmedItem.indexOf('=');
    const key = trimmedItem.substring(0, splitIndex);
    const value = trimmedItem.substring(splitIndex + 1);
    acc[key] = value;
    return acc;
  }, {})
}

// Given a cookie name, get the value of that cookie.
function getValueForCookie(cookie) {
  return parseCookies()[cookie];
}
```
