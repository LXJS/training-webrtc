# Start the Workshop!

## Overview

WebRTC enables real-time communication in the browser.

This tutorial explains how to build a simple video and text chat application.

For more information about WebRTC, see [Getting started with WebRTC](http://www.html5rocks.com/en/tutorials/webrtc/basics) on HTML5 Rocks.

You can submit feedback about the WebRTC APIs at [bit.ly/webrtcfeedback](http://bit.ly/webrtcfeedback).

## Prerequisites

Basic knowledge:

1. HTML, CSS and JavaScript
2. [git](http://git-scm.com/)
3. [Chrome DevTools](https://developers.google.com/chrome-developer-tools/)

Experience of [Node.js](http://nodejs.org/) and [socket.io](http://socket.io/) would also be useful.

Installed on your development machine:

1. Google Chrome or Firefox.
1. Code editor.
1. Webcam.
1. Git, in order to get the source code.
1. The [source code](https://github.com/LXJS/training-webrtc).
1. Node.js with socket.io and node-static. (Node.js hosting would also be an advantage -- see below for some options.)

*The instructions in this workshop assume you are using Mac OS, Linux or Windows. Unless you know what you're doing, it's probably easier not to attempt this workshop from a Chromebook!*

It would also be useful to have an Android device with Google Chrome installed in order to try out the examples on mobile.

## Running The Examples

To run any of the examples provided in the `examples` directory of this repo simply cd into the specific step directory you'd like to see locally and run

```
node server.js
```

Before you run the server, you'll need to run `npm install`.

That directory's demo will then be live [here](http://localhost:2014).

## Step 0: Get the code

Using git, clone the workshop repository onto your development computer. If you haven't used git before, there are several tutorials and reference guides available from the [git website](http://git-scm.com/).

```bash
git clone https://github.com/LXJS/training-webrtc.git
cd training-webrtc
```

## Step 1: Create a blank HTML5 document & simple server

1. Create a bare-bones HTML document called `index.html`.
1. Use [node-static](https://npmjs.org/package/node-static) to create a simple static file server that listens on port `2014` and serves index.html (and all files in the same folder).
1. Test it out by visiting [http://localhost:2014](http://localhost:2014).

When you're done (or if you get stuck), check your solution against the solution in the `examples/step1` folder.

### Solution

[examples/step1](https://github.com/LXJS/training-webrtc/tree/master/examples/step1)


## Step 2: Get video from your webcam

1. Add a video element to your page.
1. Use `navigator.getUserMedia` to capture the user's webcam.
1. Test it out [locally](http://localhost:2014) (see instructions above on running demos).

### API Docs

- [navigator.getUserMedia](https://developer.mozilla.org/en-US/docs/Web/API/Navigator.getUserMedia)

### Hints

To make `getUserMedia` work across browsers, you need to add the following code:

  ```js
  navigator.getUserMedia = navigator.getUserMedia
    || navigator.webkitGetUserMedia
    || navigator.mozGetUserMedia
    || navigator.msGetUserMedia;
  ```

`getUserMedia` is called like this:

  ```js
  navigator.getUserMedia(constraints, successCallback, errorCallback);
  ```

The constraints argument allows us to specify the media to get, in this case video only:

  ```js
  var constraints = { video: true }
  ```

If successful, the success callback is called with the video stream from the
webcam. You can then set it as the source of a video tag.

  ```js
  function successCallback (localMediaStream) {
    window.stream = localMediaStream; // stream available to console
    var video = document.querySelector('video');
    video.src = window.URL.createObjectURL(localMediaStream);
    video.play();
  }
  ```

If there was an error (like the user denied access to their webcam), then the error callback is called with an error object.

  ```js
  function errorCallback (err) {
    console.error('navigator.getUserMedia error: ', err);
  }
  ```

### Solution

[examples/step2](https://github.com/LXJS/training-webrtc/tree/master/examples/step2)

### Bonus points

1. Inspect the stream object from the console.
2. Try calling `stream.stop()`.
3. What does `stream.getVideoTracks()` return?
4. Look at the constraints object: what happens when you change it to `{ audio: true, video: true }`?
5. What size is the video element?  How can you get the video's natural size from JavaScript? Use the Chrome Dev Tools to check. Use CSS to make the video full width. How would you ensure the video is no higher than the viewport?
6. Try adding CSS filters to the video element (more ideas [here](http://html5-demos.appspot.com/static/css/filters/index.html)). For example:

  ```css
  video {
    filter: hue-rotate(180deg) saturate(200%);
    -moz-filter: hue-rotate(180deg) saturate(200%);
    -webkit-filter: hue-rotate(180deg) saturate(200%);
  }
  ```

7. Try changing constraints: see the sample at [googlechrome.github.io/webrtc/samples/web/content/getusermedia-resolution/](http://googlechrome.github.io/webrtc/samples/web/content/getusermedia-resolution/).


## Step 3: Stream video with RTCPeerConnection

`RTCPeerConnection` is the WebRTC API for video and audio calling. `RTCPeerConnection`
instances need to exchange metadata in order to set up and maintain a WebRTC 'call':

- Candidate (network, i.e. IP address and port) information.
- _Offer_ and _answer_ messages providing information about media such as resolution and
codecs.

In other words, an exchange of metadata is required before peer-to-peer audio, video or
data streaming can take place. This process is called _signaling_.

In this activity, the 'sender' and 'receiver' RTCPeerConnection objects are on the same
page, so signaling is simply a matter of passing objects between methods.

In a real world application, the sender and receiver RTCPeerConnections are not on the
same page, and we need a way for them to communicate metadata.

Here is a rough diagram of the flow of methods and events:

![flow](step3.png)

Of course, for this code challenge, there is no server. Everything is done locally, within the same page.

Your task is to set up a connection between two `RTCPeerConnection` instances on the same
page. Not much use in the real world, but good for understanding how RTCPeerConnection
works!

1. Take a look at the [munge SDP example](https://googlechrome.github.io/webrtc/samples/web/content/munge-sdp/). This will give you a concrete idea of the steps involved in a complete "signaling exchange".
1. Edit the HTML so there are two video elements and three buttons: Start, Call and Hang Up:

  ```html
  <!-- "muted" will prevent horrible audio feedback :) -->
  <video id="localVideo" autoplay muted></video>
  <video id="remoteVideo" autoplay muted></video>

  <div>
    <button id="startButton">Start</button>
    <button id="callButton">Call</button>
    <button id="hangupButton">Hang Up</button>
  </div>
  ```

1. Use `getUserMedia` and `RTCPeerConnection` to capture a video stream and send it to a
"remote" RTCPeerConnection. The buttons in the UI should do the following:
  - start button: captures webcam video stream
  - call button: creates two RTCPeerConnection objects, sets up listeners
  - hangup button: closes the peer connections
1. Test it out [locally](http://localhost:2014) (see instructions above on running demos).

### API Docs

- [RTCPeerConnection](http://docs.webplatform.org/wiki/apis/webrtc/RTCPeerConnection)
- [RTCSessionDescription](http://docs.webplatform.org/wiki/apis/webrtc/RTCSessionDescription)
- [RTCIceCandidate](http://docs.webplatform.org/wiki/apis/webrtc/RTCIceCandidate)

### Hints

- To make `RTCPeerConnection` work across browsers, you need to add the following code:

  ```js
  var RTCPeerConnection = window.mozRTCPeerConnection
    || window.RTCPeerConnection
    || window.webkitRTCPeerConnection;

  var RTCSessionDescription = window.mozRTCSessionDescription
    || window.RTCSessionDescription
    || window.webkitRTCSessionDescription;

  var RTCIceCandidate = window.mozRTCIceCandidate
    || window.RTCIceCandidate
    || window.webkitRTCIceCandidate;
  ```

- The "offers" and "answers" are in [SDP (Session Description
Protocol)](http://en.wikipedia.org/wiki/Session_Description_Protocol) format. They specify
the capabilities and media of each `RTCPeerConnection`.

- The "ice candidates" are messages from the [ICE (Interactive Connectivity Establishment
Protocol)](http://en.wikipedia.org/wiki/Interactive_Connectivity_Establishment). They are
basically IP address and port pairs that the remote peer should attempt to connect to.

### Solution

[examples/step3](https://github.com/LXJS/training-webrtc/tree/master/examples/step3)

### Bonus points

1. Take a look at _chrome://webrtc-internals_. (There is a full list of Chrome URLs at _chrome://about_.)
2. Style the page with CSS:
  - Put the videos side by side.
  - Make the buttons the same width, with bigger text.
  - Make sure it works on mobile.
3. From the Chrome Dev Tools console, inspect _localStream_, _localPeerConnection_ and _remotePeerConnection_.
4. Take a look at _localPeerConnection.localDescription_. What does SDP format look like?


## Step 4: Stream arbitrary data with RTCDataChannel

For this step, we'll use RTCDataChannel to send text between two textareas on the same page. Not very useful, except to demonstrate how the API works.

1. Create a new document and add the following HTML:

  ```html
  <textarea id="dataChannelSend" disabled></textarea>
  <textarea id="dataChannelReceive" disabled></textarea>

  <div id="buttons">
    <button id="startButton">Start</button>
    <button id="sendButton">Send</button>
    <button id="closeButton">Stop</button>
  </div>
  ```

1. Set up two RTCPeerConnections, just like you did for step 3.
1. Call `createDataChannel(channelName)` on the first peer connection. It will return a data channel.
1. To get the data channel from the remote peer connection, listen for the `datachannel` event.
1. Test it out [locally](http://localhost:2014) (see instructions above on running demos).

### API Docs

- [RTCPeerConnection](http://docs.webplatform.org/wiki/apis/webrtc/RTCPeerConnection)
- [RTCDataChannel](http://docs.webplatform.org/wiki/apis/webrtc/RTCDataChannel)

### Hints

Use RTCPeerConnection and RTCDataChannel to enable exchange of text messages.

Most of the code in this section is the same as for the RTCPeerConnection example. Additional code is as follows:

  ```js
  function sendData(){
    var data = document.getElementById("dataChannelSend").value;
    sendChannel.send(data);
  }

  ...

  localPeerConnection = new RTCPeerConnection({ iceServers: [] });
  sendChannel = localPeerConnection.createDataChannel('sendDataChannel');
  sendChannel.onopen = handleSendChannelStateChange;
  sendChannel.onclose = handleSendChannelStateChange;

  ...

  remotePeerConnection = new RTCPeerConnection({ iceServers: [] });
  function gotReceiveChannel(event) {
    receiveChannel = event.channel;
    receiveChannel.onmessage = gotMessage;
  }

  ...

  remotePeerConnection.ondatachannel = gotReceiveChannel;
  function gotMessage(event) {
    document.getElementById("dataChannelReceive").value = event.data;
  }
  ```

The syntax of RTCDataChannel is deliberately similar to WebSocket, with a `send()` method and a `message` event.

### Solution

[examples/step4](https://github.com/LXJS/training-webrtc/tree/master/examples/step4)

### Bonus points

1. Try out RTCDataChannel file sharing with [Sharefest](http://www.sharefest.me/). When would RTCDataChannel need to provide reliable delivery of data, and when might performance be more important -- even if that means losing some data?
1. Use CSS to improve page layout, and add a placeholder attribute to the _dataChannelReceive_ textarea.
1. Test the page on a mobile device.


## Step 5: Set up a signaling server and exchange messages

RTCPeerConnection instances need to exchange metadata (candidates, offers, answers) in order to set up and maintain a WebRTC 'call'. This metadata exchange is required before peer-to-peer audio, video or data streaming can take place. As discussed before, this process is called _signaling_.

In the examples already completed, the 'sender' and 'receiver' RTCPeerConnection objects are on the same page, so signaling is simply a matter of passing objects between methods.

In a real world application, the sender and receiver RTCPeerConnections are not on the same page, and we need a way for them to communicate metadata.

For this, we use a signaling server: a server that can exchange messages between a WebRTC app (client) running in one browser and a client in another browser. The actual messages are stringified JavaScript objects.

**To reiterate: metadata exchange between WebRTC clients (via a signaling server) is required for RTCPeerConnection to do audio, video and data streaming (peer to peer).**

In this step we'll build a simple Node.js signaling server, using the `socket.io` Node module and JavaScript library for messaging. Experience of [Node.js](http://nodejs.org/) and [socket.io](http://socket.io/) will be useful, but not crucial -- the messaging components are very simple. In this example, the server (the Node app) is _server.js_ and the client (the web app) is _index.html_.

The Node server application in this step has two tasks.

To act as a messaging intermediary:

  ```js
  socket.on('message', function (message) {
    log('Got message: ', message);
    socket.broadcast.emit('message', message);
  });
  ```

To manage WebRTC video chat 'rooms':

  ```js
  if (numClients == 0) {
    socket.join(room);
    socket.emit('created', room);
  } else if (numClients == 1) {
    io.sockets.in(room).emit('join', room);
    socket.join(room);
    socket.emit('joined', room);
  } else { // max two clients
    socket.emit('full', room);
  }
  ```

Our simple WebRTC application will only permit a maximum of two peers to share a room.

1. Ensure you have Node, socket.io, [node-static](https://www.npmjs.org/package/node-static) installed.

  ```bash
  npm install socket.io
  npm install node-static
  ```

1. Write a simple signalling server that allows two clients to exchange signalling messages. For this step, you don't need to use any WebRTC APIs on the client-side.
1. To start your server when you're finished, run the following command from a terminal in your application directory:

  ```bash
  node server.js
  ```

1. From your browser, open _localhost:2014_. Open a new tab page or window in any browser and open _localhost:2014_ again, then repeat.
1. To see what's happening, check the Chrome DevTools console (Command-Option-J, or Ctrl-Shift-J).
1. Take a look at the code in the [examples/step5](examples/step5) directory if you get stuck.

### Solution

[examples/step5](https://github.com/LXJS/training-webrtc/tree/master/examples/step5)

### Bonus points

1. Try deploying your messaging server so you can access it via a public URL. (Free trials and easy deployment options for Node are available on several hosting sites including [nodejitsu](http://www.nodejitsu.com), [heroku](http://www.heroku.com) and [nodester](http://www.nodester.com).)

2. What alternative messaging mechanisms are available? (Take a look at [apprtc.appspot.com](http://apprtc.appspot.com).) What problems might we encounter using 'pure' WebSocket? (Take a look at Arnout Kazemier's presentation, [WebSuckets](https://speakerdeck.com/3rdeden/websuckets).)

3. What issues might be involved with scaling this application? Can you develop a method for testing thousands or millions of simultaneous room requests.

4. Try out Remy Sharp's tool [nodemon](https://github.com/remy/nodemon). This monitors any changes in your Node.js application and automatically restarts the server when changes are saved.

5. The solution uses a JavaScript prompt to get a room name. Work out a way to get the room name from the URL, for example _localhost:2014/foo_ would give the room name _foo_.


## Step 6: RTCPeerConnection with messaging

In this step, we build a video chat client, using the signaling server we created in Step 5 and the RTCPeerConnection code from Step 3.

1. Ensure you have Node, socket.io and [node-static](https://github.com/cloudhead/node-
static) installed and working. If in doubt, try the code in Step 5.
1. Using the code from your _step 3_ and _step 5_ solutions as a starting point, write a
complete app that allows two clients to do a video/audio chat.
1. Run your server with:

  ```bash
  node server.js
  ```

1. From your browser, open [localhost:2014](http://localhost:2014). Open a new tab page or window and open [localhost:2014](http://localhost:2014) again.
1. View logging from the Chrome DevTools console and WebRTC debug information from chrome://webrtc-internals.

### Solution

**This solution users [adapter.js](https://github.com/LXJS/training-webrtc/tree/master/examples/step6/js/lib/adapter.js). This is a [JavaScript shim](http://stackoverflow.com/questions/6599815/what-is-the-difference-between-a-shim-and-a-polyfill), maintained by Google, that abstracts away browser differences and spec changes.**

[examples/step6](https://github.com/LXJS/training-webrtc/tree/master/examples/step6)

### Bonus points

1. This application only supports one-to-one video chat. How might you change the design to enable more than one person to share the same video chat room? (Look at [talky.io](http://talky.io) for an example of this in action.)

2. The solution has the room name _foo_ hard coded. What would be the best way to enable other room names?

3. Does the app work on mobile? Try it out on a phone, on a 7" and a 10" tablet. What layout, UI and UX changes would be required to ensure a good mobile experience?

4. Deploy your app at a public URL (see above for hosting options). Try different network configurations, for example with one user on wifi and another on 3G. Any problems?

5. How would users share the room name? Try to build an alternative to sharing room names.


## Step 7: Putting it all together: RTCPeerConnection + RTCDataChannel + signaling

This is a DIY step!

1. Take a look at the app you built in step 4.
1. Add the RTCDataChannel code to your Step 6 app to create a complete application.

### Solution

[examples/step7](https://github.com/LXJS/training-webrtc/tree/master/examples/step7)

### Bonus points

1. Consider separating the WebRTC complexity into it's own separate file or "module". This
way, the rest of the video chat application doesn't need to understand the WebRTC
internals. An example of doing this well is [simple-peer](https://github.com/feross/simple-peer).
1. The app hasn't had any work done on layout. Make it look pretty!
1. Make sure your app works well on different devices.
1. Test out Chrome <-> Firefox interop. It should work!


## Step 8: Use a WebRTC library: SimpleWebRTC

Abstraction libraries such as SimpleWebRTC make it simple to create WebRTC applications.

1. Create a new document using the code from [examples/step8/index.html](https://github.com/LXJS/training-webrtc/tree/master/examples/step8/index.html).
2. Open the document in multiple windows or tab.

### Solution

[examples/step8](https://github.com/LXJS/training-webrtc/tree/master/examples/step8)

### Bonus points

1. Find a WebRTC library for RTCDataChannel. (Hint: there's one named PeerJS!)
2. Set up your own signaling server using the SimpleWebRTC server [signalmaster](https://github.com/andyet/signalmaster).


## Credit

This workshop was adapted by [@feross](https://twitter.com/feross) and [@HCornflower](https://twitter.com/HCornflower) from the excellent [webrtc/workshop](https://bitbucket.org/webrtc/workshop/) repo, by the webrtc project. It was updated and expanded for this LXJS workshop!
