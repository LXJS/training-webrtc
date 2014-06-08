# ![webrtc](http://www.webrtc.org/_/rsrc/1318870658554/config/customLogo.gif?revision=8) LXJS 2014 Workshop

*"Imagine a world where your phone, TV and computer could all communicate on a common platform. Imagine it was easy to add video chat and peer-to-peer data sharing to your web application. That's the vision of WebRTC." — Sam Dutton*

**WebRTC** (Web Real-Time Communication) is an API drafted by the World Wide Web Consortium (W3C) that supports browser-to-browser applications for voice calling, video chat, and P2P file sharing without plugins.

## Overview

### Topics

In this workshop at LXJS 2014, we will cover:

- What is WebRTC?
- What types of apps and features does WebRTC enable you to build?
- How to create WebRTC video/voice chat apps
  - How to create peer-to-peer connections in the browser
  - How to use `getUserMedia` to capture the user's webcam and microphone
  - How the "signaling process" allows us to connect two peers, and why it's necessary
  - How to write server-side (node.js) code to facilitate the signaling process
- How to create WebRTC data channel apps
  - How to send binary and text data
  - How to create reliable (tcp-like) and unreliable (udp-like) data channels
- How to handle browser differences

## Get excited

### Products using WebRTC

Check out some of the real-world products that make use of WebRTC:

- Simple video chat - [Talky](http://talky.io/) / [AppRTC](https://apprtc.appspot.com/)
- Simple file sharing - [ShareFest](http://sharefest.me)
- Peer-to-peer CDN - [PeerCDN](http://peercdn.com) / [Peer5](http://peer5.com) / [Swarmify](http://swarmify.com/) / [StreamRoot](http://www.streamroot.io/)
- Browse websites together with friends - [TogetherJS](https://togetherjs.com/)
- [Chromecast](http://www.webrtcworld.com/topics/from-the-experts/articles/347900-chromecast-webrtc.htm) - browser tab casting
- [Amazon Mayday](http://webrtchacks.com/mayday-trace/) - live kindle support
- [Snapchat](http://www.webrtcworld.com/topics/webrtc-world/articles/378013-wheelings-dealings-snapchat-acquires-webrtc-company-addlive.htm) - push-to-start video chat in a native app

### Experimental WebRTC Products

Mad scientists are pushing WebRTC to its limits. Check out these crazy projects:

- [Peer-Server](http://www.peer-server.com/) - a server backend in the browser
- [WebTorrent](http://webtorrent.io) - a streaming bittorrent client in the browser
- [WebRTC Plugin for old browsers](https://temasys.atlassian.net/wiki/display/TWPP/WebRTC+Plugins) - so you can make WebRTC work on IE9/10/11 and Safari

### WebRTC Vendors

- [AT&T](https://js.att.io/)
- [GoInstant](https://developers.goinstant.com/v1/widgets/audio_and_video/index.html)
- [Tokbox](http://tokbox.com/opentok/intro/)


## Sound awesome!?

Great! Here's how to get ready.

### Pre-Workshop Preparation

In order to prepare for this workshop, you should read the following articles before arriving at LXJS! If you have a question, please [open an issue](https://github.com/LXJS/training-webrtc/issues) and we will be glad to answer. You might be helping other participants!

### Todo List

- [ ] Check out [talky.io](https://talky.io/) and [sharefest.me](https://www.sharefest.me/)
- [ ] Check out the [first WebRTC call ever made](https://www.youtube.com/watch?v=MsAWR_rJ5n8). Historical!
- [ ] Read [Getting Started with WebRTC](http://www.html5rocks.com/en/tutorials/webrtc/basics/)
- [ ] Watch [Google I/O 2013 WebRTC presentation](https://www.youtube.com/watch?v=p2HzZkd2A40)
- [ ] Complete activities in "WebRTC Voodoo" workshopper -- coming soon...

### Additional Resources

These are not required, but if you want to hack on WebRTC code before you get to LXJS, you should check out the following links (with sample code!)

- [Cross-browser video/audio (adapter.js)](https://code.google.com/p/webrtc/source/browse/trunk/samples/js/base/adapter.js?r=3905)
- [Cross-browser data channel (webrtc-peer)](https://github.com/quartzjer/webrtc-peer/)

## Hi, I'm Feross!

![feross](https://avatars3.githubusercontent.com/u/121766?s=300)

I'll be your trainer! :) I am currently building [WebTorrent](http://webtorrent.io), a streaming BitTorrent client for the browser, powered by WebRTC. Before that, I built [PeerCDN](https://peercdn.com/), a peer-to-peer content delivery network to makes sites faster and cheaper (which was acquired by Yahoo). Check out my blog at [feross.org](http://feross.org).

## 28 jun - 17:30h Participants

- Abel Soares - [abelsoares](https://github.com/abelsoares)
- Bruno Abrantes - [inf0rmer](https://github.com/inf0rmer)
- David Cruz - [dcruz](https://github.com/dcruz)
- Dominic Lüchinger - [dol](https://github.com/dol)
- Franz Enzenhofer - [franzenzenhofer](https://github.com/franzenzenhofer)
- Igor Soarez - [soarez](https://github.com/soarez)
- João Jerónimo - [joaojeronimo](https://github.com/joaojeronimo)
- Jorge Monteiro - [jorgemonteiro](https://github.com/jorgemonteiro)
- Leonardo Aretakis - [leoaretakis](https://github.com/leoaretakis)
- Luís Ferreira - [zamith](https://github.com/zamith)
- Luke Bond - [lukebond](https://github.com/lukebond)
- Max Gfeller - [MaxGfeller](https://github.com/MaxGfeller)
- Miguel Serrano - [miguelvps](https://github.com/miguelvps)
- Miguel Palhas - [naps62](https://github.com/naps62)
- Nuno Costa - [naflcosta](https://github.com/naflcosta)
- Paulo Miranda - [pauloabmiranda](https://github.com/pauloabmiranda)
- Robert Kowalski - [robertkowalski](https://github.com/robertkowalski)
- Rogério Vicente - [rogeriopvl](https://github.com/rogeriopvl)
- Ronaldo Sousa - [ronaldofs](https://github.com/ronaldofs)
- Sandro Maio - [sandromaio](https://github.com/sandromaio)
- Tim Park - [timfpark](https://github.com/timfpark)
- Tom Cartwright - [tomcartwrightuk](https://github.com/tomcartwrightuk)

## 27 jun - 14:30h Participants

- Charlie Robbins - [indexzero](https://github.com/indexzero)
- David McMullin - [davecocoa](https://github.com/davecocoa)
- Dominykas Blyžė - [dymonaz](https://github.com/dymonaz)
- Frederic Hemberger - [fhemberger](https://github.com/fhemberger)
- George Shank - [taterbase](https://github.com/taterbase)
- Igor Soarez - [soarez](https://github.com/soarez)
- J Oates - [joates](https://github.com/joates)
- James Wood - [jamesjwood](https://github.com/jamesjwood)
- João Nelas - [adagios](https://github.com/adagios)
- João Reis
- Joaquim Serafim - [joaquimserafim](https://github.com/joaquimserafim)
- John Brett - [johnbrett](https://github.com/johnbrett)
- Jorge Dias - [diasjorge](https://github.com/diasjorge)
- Luis Naia
- Luis Confraria - [luisbug](https://github.com/luisbug)
- Matteo Collina - [mcollina](https://github.com/mcollina)
- Matthias Knoll - [kohlikohl](https://github.com/kohlikohl)
- Miguel Coquet - [mcoquet](https://github.com/mcoquet)
- Pierre Ozoux - [pierreozoux](https://github.com/pierreozoux)
- Ricardo Tomasi - [ricardobeat](https://github.com/ricardobeat)
- Ricardo Melo - [rjsmelo](https://github.com/rjsmelo)
- Ricardo Soares - [rsoares](https://github.com/rsoares)
- Sebastian Golasch - [asciidisco](https://github.com/asciidisco)
- Tracy Hinds - [hackygolucky](https://github.com/hackygolucky)
- Zoltan Feher - [zkiiito](https://github.com/zkiiito)
