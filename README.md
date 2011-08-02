# App Cloud Emulator #

## Overview

App Cloud Emulator is a tool for encouraging in-browser development of App Cloud apps. It emulates a native device (as much as possible) so most development can be in-browser leading to faster turn-around and better tools.

Features:

* Displays your application inside the device with the same resolution as on-device.
* Toggle between portrait and landscape orientations. Change in orientation triggers the same JS events the device API would normally.
* Toggle between iPhone and Android devices (back button support for Android).
* Support for tap/click and scroll (provided by default).
* Buttons for firing swipe left/right events on the current view.
* Access to all views included in the manifest.xml with icon (if provided).
* Access to the App Cloud API object via the JavaScript console.
* Easy installation: just drop it in your application root. Only used in development and doesn't have any effect on production (other than the file size which is about ~500KB total).

See [this video](http://bcove.me/ou9gf5n5 "App Cloud Emulator Demo") to see it in action.

## Installation

1. Download the zip file and extract into your app root
2. Go to /emulator/ at your application root URL
3. Enjoy!

Note that many (read: all) apps need to be able to make AJAX requests cross-domain (either to Brightcove or elsewhere) which is, by default, disable in the browser. For Chrome, start up with the --disable-web-security flag:

    $ /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --disable-web-security

## Tips

### Access to the Brightcove API

The 'bc' object in the frame is made available in the outer frame. Try it out in the JavaScript console in your browser:

    bc.ui.width()

### Better browser support in your app

While this should be improving in the core API over time, you are always free to override the API when working in-browser to make life easier for yourself:


	if (!bc.device.isNative()) {
		bc.device.getLocation = function(success, error) {
			success({"latitude":'42.330454', "longitude":'-71.193073'});
		};

		bc.device.alert = function(message, success, error) { alert(message); };

		bc.device.setAutoRotateDirections = function( directions, successCallback, errorCallback ) {};
	}
