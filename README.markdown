MumbleKit - A Mumble client framework for iOS and Mac OS X
==========================================================

What's this?
------------

This is the source code of MumbleKit - a Mumble client framework
for iOS-based devices and computers running Mac OS X.

Mumble is gaming-focused social voice chat utility. The desktop
version runs of Windows, Mac OS X, Linux and various other Unix-like
systems. Visit its website at:

 <http://mumble.info/>

Fetching dependencies
---------------------

To build this you need the latest version of Xcode from Apple.
These days, Xcode is distributed through the Mac App Store.

Before starting your build, you will need to check out the re-
quired submodules.

    $ git submodule init
    $ git submodule update

This will fetch known "working" snapshot of CELT, Speex and
Protocol Buffers for Objective C.

How do I include this into my Swift Xcode project? (iOS, Xcode 9.3)
-----------------------------------------------------------

* In XCode, create a project in a workspace. Choose "Single-Page app", using Swift.
Example folder: Documents/SampleProject

* Clone MumbleKit
This can be in a directory separate from the project dir, e.g. Documents/MumbleKit.

* Open a terminal at the MumbleKit folder and retrieve submodules:
	- git submodule init
	- git submodule update

* In XCode, create a folder (group) called "Dependencies" inside your own project in the Project Navigator.

* Open the MumbleKit folder in finder. Drag the MumbleKit.xcodeproj file into the Dependencies group in XCode.

* Build the MumbleKit project: Choose the scheme "MumbleKit (iOS)" in the XCode top bare and build. If you get a lot of project settings recommendations, go through them and fix them one by one.

* In the MumbleKit group, right-click and select "Add files to MumbleKit.xcodeproj". Find the MumbleKit/src/MumbleKit.pch file. Select to add it to the MumbleKit (iOS) target.

* In the MumbleKit project settings, select Build Settings, item "Prefix Header": Add the path to the MumbleKit.pch file: `src/MumbleKit.pch`

* Select your project in the Project Navigator to open the project settings page. In this, select the Build Phases tab. In "Target Dependencies", press the + button and select the "MumbleKit (iOS)" item.

* In the Build Settings, find the "Other linker flags" and add '-lc++'.

* In the Build Settings, find the "Header Search Paths" and add an entry: "$(SRCROOT)/../MumbleKitForked/src". SRCROOT is the root folder for your own project, and this example has MumbleKit in a folder called MumbleKitForked next to my own project folder.

* Add a Bridging Header to your project: New File->Header file. Call the file BridgingHeader.h. Clear the contents of the file.

* Configure the project to use the Bridging header: In Build Settings, find the "Objective-C Bridging Header" entry and specify the chosen file: "$(SRCROOT)/SampleProject/BridgingHeader.h" (exchange SampleProject for your own project name)

* Open the Bridging Header file and add: 

```
#import <Foundation/Foundation.h>
#import <MumbleKit/MKConnection.h>
```

Add an import statement for each MumbleKit class that you reference from Swift Code. It might be all of them.

* In your project, in Build Phases, add Link Binary With Libraries:
Security.framework
CFNetwork.framework
AudioToolbox.framework
libMumbleKit.a

* The build should now work.

How do I include this into my Xcode project? (Mac OS X, Xcode 4)
----------------------------------------------------------------

One way to do this is to include MumbleKit.xcodeproj inside your main project. Then:

 * Make MumbleKit (Mac) a direct dependency of your chosen target.

 * Add MumbleKit.framework to the 'Link Binary With Libraries' section of your chosen target's
   build phases.

 * Add a copy build phase. Copy MumbleKit.framework into 'Frameworks'.
