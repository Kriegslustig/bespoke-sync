# bespoke-sync
## Cross-client synchronization for [Bespoke.js](https://github.com/markdalgleish/bespoke.js) presentations

Setup with Server Sent Events (for Server -> Client communication) and plain XMLHttpRequests (for Client -> Server communication).

Can be used to setup two screens (e.g. one for audience one for presenter) in sync:  
Audience screen:                            Your screen:

<img src="presentation.gif" />

Above demo uses [bespoke-notes](https://github.com/medikoo/bespoke-notes#bespoke-notes) plugin to display notes on presenter's laptop screen

### Usage

#### Server

Use returned middleware as in example below. You can use it directly in your server handler, or handle it with [Connect](http://www.senchalabs.org/connect/)

```javascript
var bespokeSyncMiddleware = require('bespoke-sync/server')({
  // Options (all optional, with defaults as below)
  log: false,
  ssePath: '/sse-slides/',
  xhrPath: '/slide/'
});

createServer(function (req, res) {
	bespokeSyncMiddleware(req, res, function () {
	  // Request not handled by Bespoke, handle below
	  // ...
	});
});
```

#### Client (browser)

```javascript
var sync = require('bespoke-sync/client');

bespoke.from(selector, [
	// Options (all optional, with defaults as below)
  sync({
    log: false,
    ssePath: '/sse-slides/', // Must match ssePath in server conf
    xhrPath: '/slide/' // Must match xhrPath in server conf
  })
]);
```

### Installation
#### npm

In your presentation path:

	$ npm install bespoke-sync
