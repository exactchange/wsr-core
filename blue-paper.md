# WSR Technical Overview

## Features

### WebSocket Relay (WSR) Protocol

The new WSR protocol extends WS by introducing behavioral types for served content. Like with HTTP & WS, the transfer object is a message `string`, the format of which is defined by its respective Behavior & Content Types.

**Behavior Types**

- Save
  - Default behavior for: \*
  - Applies to: \*
- View
	- Default behavior for: media/jpg|png|svg|mp3|mp4, text/\*, interactive/html
	- Applies to: \*
- Run
	- Default behavior for: interactive/rbx
	- Applies to: media/\*, interactive/\*

Syntax:
```
  type:<behavior_type>, data:<content_type>/<file_format>, <encoding>, <data>
```

Examples:
```
  type:save, data:unknown/zip; zip, 504b 0304 1400 0000 0000 ... e92c (download a file)
  type:save, data:image/png; base64, iV00wANSggEUgAAggGGw0wKA ... A (download a file)

  type:view, data:video/mp4; base64, iV0KAANSUhEUgAAggGGw0wKKUUA ... A (view in a player)
  type:view, data:text/json; none, { "hello_world": "true" } (view in a text area)
  type:view, data:text/html; none, <div>hello world</div> (view in a text area)
  type:view, data:interactive/html; none, <div>hello world</div> (render HTML/CSS in a view area)

  type:run, data:interactive/rbx; none, @head ... (run RBX code)
  type:run, data:interactive/html; none, !doctype ... (run HTML/CSS/JS code)
```

**WSR Request**

```
  interface WSRRequest {
    node: Namespace;
    service?: string;
    action?: string;
    argument?: string;
  }
```
