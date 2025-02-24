# webview\_flutter\_web

This is an implementation of the [`webview_flutter`](https://pub.dev/packages/webview_flutter) plugin for web.

It is currently severely limited and doesn't implement most of the available functionality.
The following functionality is currently available:

- `loadRequest`
- `loadHtmlString` (Without `baseUrl`)
- `addJavaScriptChannel`
- `removeJavaScriptChannel`

Nothing else is currently supported.

## Usage

This package is not an endorsed implementation of the `webview_flutter` plugin
yet, so it currently requires extra setup to use:

* [Add this package](https://pub.dev/packages/webview_flutter_web/install)
  as an explicit dependency of your project, in addition to depending on
  `webview_flutter`.

Once the step above is complete, the APIs from `webview_flutter` listed
above can be used as normal on web.

### JavaScript channels

Contrary to the Android and iOS implementations, the `addJavaScriptChannel`
method does not create a named channel; the channel can only be accessed using
`window.parent`. In order to send a cross-platform message over a channel named
`flutterApp`, the following construction can be used in the web application:

```ts
if (window.flutterApp) {
  window.flutterApp.postMessage(message);
} else if (window.parent) {
  window.parent.postMessage(message, targetOrigin);
}
```

## Tests

Tests are contained in the `test` directory. You can run all tests from the root
of the package with the following command:

```bash
$ flutter test --platform chrome
```

This package uses `package:mockito` in some tests. Mock files can be updated
from the root of the package like so:

```bash
$ flutter pub run build_runner build --delete-conflicting-outputs
```