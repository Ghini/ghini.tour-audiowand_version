ghini.tour
====================

audio and geographic tour through a garden

idea
--------------------

we want to offer visitors something functionally similar to the audio tours that most musea, at least in Europe, offer.

you see a plate in the garden, grab the guide, type the number shown on the plate, you get to hear an explanation in your language.

realization
--------------------

we plan to use rogerhyam/audiowand

roadmap
--------------------

* audiowand works on android,
* android is mostly based on java and audiowand follows the guideline.
* instructions on audiowand point you to the instructions on cordova
* cordova does not mention how to install android

* since audiowand only offers android, it would be reasonable to point the
  developer to how to install the Andoird SDK

in order to just start setting up the sdk, you need to download such a large
amount of data that I never yet managed to find the time to do it.

1. jdk
2. cordova
3. android

if you try to ``cordova build android``, you get this::

    Error: Failed to find 'ANDROID_HOME' environment variable. Try setting setting it manually.
    Detected 'adb' command at /usr/bin but no 'platform-tools' directory found near.
    Try reinstall Android SDK or update your PATH to include valid path to SDK/platform-tools directory.

- read `these instructions <https://developer.android.com/studio/install.html>`_
- download android studio 
- unpack it
- start it  
- be prepared to download 1G+ of more data

- Once you have installed Android Studio, you use it to download the Android SDK's.
- Tools -> Android -> SDK Manager

- decide which android versions you want to support. end of 2016 it's `still
  strongly advisable
  <http://www.androidpolice.com/2016/12/05/android-platform-distribution-december-2016-kitkat-is-finally-toppled-nougat-doesnt-move-much/>`_
  to support 4.4 (24%), while 4.1,2,3 form together more than 12% of the
  running devices. in July 2017 these figures went down to respectively
  18.1% and 8.8%.
- Android Studio puts the SDKs somewhere in your computer, check the
  location. for me, it was at ~/Android/Sdk. let ANDROID_HOME point here.
  
- cordova also needs gradle to be in the path. create a symlink
  ``/opt/android-studio/gradle/gradle-3.2/bin/gradle`` to ``/usr/local/bin``

- start ``cordova build android`` and be prepared to wait. the first run might take 20 minutes.
- start ``cordova build android --release`` when your tour is ready to be released.

- you might need to use ``cordova prepare``, I'm not sure what that really means.

keeping track of tours
----------------------------

if you follow the current audiowand instructions, your tours will not be
under source control, and you will end with as many checkouts of the
audiowand sources as your tours. both things are not particularly desirable,
and I suggest we do things slightly differently.

- create your tour under version control,
- initialize its data directory from the core template audiowand application,
- go back to your cordova project,
- symlink the content of this directory (not the directory itself, it won't work) into ``www/data``
