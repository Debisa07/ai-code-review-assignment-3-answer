## What was the bug?

`Client.request(..., api=True)` failed to attach an `Authorization` header when `self.oauth2_token` was a dictionary. The request went out without a bearer token.

## Why did it happen?

Refresh logic only ran when the token was missing or when it was an expired `OAuth2Token` instance. A non-empty dict bypassed both checks, so `refresh_oauth2()` was not called. The header-setting branch only handled `OAuth2Token`, so no auth header was added.

## Why does your fix actually solve it?

The condition now refreshes unless `self.oauth2_token` is an `OAuth2Token` and still valid. That forces dict tokens through `refresh_oauth2()`, which replaces them with a valid `OAuth2Token`, and the existing header branch then sets `Authorization` correctly.

## One realistic edge case not covered

A caller can pass a `headers` dict that already includes `Authorization`; current tests do not verify whether API mode should override that value or preserve it.