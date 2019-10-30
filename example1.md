## Interaction 0: GET /path/to/resource

### Request headers recorded for playback:

```
Header1: something
Header2: something else
```

### Request body recorded for playback (application/xml):

```
<hello>
  <how-are-you/>
</hello>
```

### Response headers recorded for playback:

```
Content-Type: text/plain
Connection: keep-alive
Set-Cookie: CookieName=CookieValue
Header-X: abc-123
```

### Response body recorded for playback (200: application/json):

```
Mary had a little lamb
```

## Interaction 1: POST /path/to/another/thing

### Request headers recorded for playback:

...

### Request body recorded for playback ():

...

### Response headers recorded for playback:

...

### Response body recorded for playback (200: application/json):

...

## Interaction 2: GET /path/to/yet/another

... and so on ...


