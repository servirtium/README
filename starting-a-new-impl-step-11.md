## Have a raw serve (GET) capability for static content

Servierium should be able to mark a specific directory as sttic content and not record it at all (or play it back)

```
servirtium.staticContent("path/in/local/file/system/", "/directoryOnServitiumServerThatBypassesRecoding");
```

* Local FS path is relative or absolute.  
* Mapped path for the servirtium server is from root and could have slashes, but few would use that.

You would point Selenium/Cypress/Playright etc at this.
