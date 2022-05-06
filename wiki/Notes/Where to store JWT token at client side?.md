### Option 1 - Web storage (localStorage or sessionStorage)
**Pros**

- The browser will not automatically include anything from the Web storage into HTTP requests making it not vulnerable to CSRF.

- can only be accessed by JS running in the exact same domain that created the data.

- Allows to use the most semantically correct approach to pass token authentication credentials in HTTP (the Authorization header with a Bearer scheme).

- It's very easy to cherry pick the request that should contain authentication token.

**Cons**

- Can not accessed by JS running in sub-domain of the on that created the data (a value written by `example.com` can not be read by `sub.example.com`).
 
- 🚨 Is vulnerable to XSS.

- In order to perform authenticated requests you can only use browser/library API's that allow for you to customize the request (pass the token to `Authorization` header).

### Option 2 - Http-Only cookie

**Pros**

- It's not vulnerable to XSS.

- The browser automatically includes the token in any request that meets the cookie specification (domain, path and lifetime).

- The cookie can be created at a top-level domain and used in requests performed by sub-domains.

**Cons**

- 🚨 It's vulnerable to CSRF.

- You need to be aware and always consider possible usage of cookies in sub-domains.

- Cheery picking the request that should include the cookie is doable but messier.

- You may (still) hit some issues with small differences in how browsers deal with cookies.

- 🚨 if you're not carefully you may implement CSRF mitigation strategy that is vulnerable to XSS.

- The server-side needs to validate a cookie for authentication instead of more appropriate `Authorization` header.

**Usage**

You don't need to do anything in client-side as the browser will automatically take care of things for you.

### Option 3 - Javascript accessible cookie (which is ignored by server-side)