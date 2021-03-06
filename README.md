#Taplytics-Android SDK

_Taplytics is a native mobile A/B testing and push notification platform that helps you optimize your Android app!_ 

**[Get started with Taplytics](https://taplytics.com/docs/android-sdk/getting-started)** | **[View the Javadoc](https://s3.amazonaws.com/cdn.taplytics.com/javadoc/index.html)**

###**Current Version: [1.9.7](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.9.7)** |   	 [FAQ](https://github.com/taplytics/Taplytics-Android-SDK/blob/master/FAQ/FAQ.md)

###Big News: [Push has changed and is better in 1.9.+](https://github.com/taplytics/Taplytics-Android-SDK/blob/master/FAQ/push%20update.md)

###Big News: Retrofit2 can be used in place of Volley in 1.8.0+ (Optional).

## Getting Started

_How do I, as a developer, start using Taplytics?_

1. _Sign up for a free account at [Taplytics.com](https://taplytics.com?utm_source=github&utm_campaign=documentation&utm_medium=content)._
2. _Install the SDK. Steps [here](/START.md)._
3. Create [Experiments](/EXPERIMENTS.md) or send [Push Notifications](/PUSH.md) to your users!

## Changelog

**[1.9.7](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.9.7)**

1. Button click goals in RecyclerViews/ListViews


**[1.9.6](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.9.6)**

1. Added timeouts to ExperimentsLoadedListener and RunningExperimentsListener.

**[1.9.5](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.9.5)**

1. Fixed an issue with 'Time on View' goals. 
2. Fixed an issue where support fragments were sometimes counting opens twice.
3. Added more animals to the proguard file. Specifically birds. _Very important._

**[1.9.3](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.9.3)**

1. Use an extremely unique ID instead of possibly non-unique device settings and information. 
2. Upgraded SDK to Android 24. DID NOT compile with jack, so that you can still use java 7 if you wish. 
3. Button click conversions fix!
4. Sessions less easy to re-trigger.

**[1.9.2](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.9.2)**

1. Android sometimes sets a device ID to `0123456789ABCDEF` on Chinese devices, custom ROMs, and emulators. This was breaking distributions as they were all seen as the same device. This has been fixed.
2. fixed delayComplete() being called twice.

**[1.9.1](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.9.1)**

1. Simply a version number bump to allow a fix for #15 if needed on CI.

**[1.9.0](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.9.0)**

1. Workaround for when view ids change in release mode vs debug mode.
2. **[Big new push notification changes.](https://github.com/taplytics/Taplytics-Android-SDK/blob/master/PUSH.md#4-custom-data-and-tracking-push-interactions)**
3. Socketio safety.
4. Fully deprecated code experiments. Use code blocks and dynamic variables now.
5. General code cleanup.


**[1.8.3](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.8.3)**

1. Can now use JSONObjects as Dynamic Variables.

**[1.8.2](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.8.2)**

1. _Faster_ button click detection!

**[1.8.1](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.8.1)**

1. Fixed a problem accessing Mixpanel Tokens. 

**[1.8.0](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.8.0)**

1. You can now use Retrofit2 if you wish and remove volley. More info [here](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.8.0)
2. getRunningExperimentsAndVariations will no longer return null, and will instead return an empty HashMap in the event that the configuation has not been loaded.
3. Fixed a race condition in which a session ID could be null if it the config was being loaded at the same time as the appUser being reset.

**[1.7.24](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.24)**

1. Improved view change timing on support fragments to allow for guaranteed first-load changes in most cases.

**[1.7.23](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.23)**

1. Fixed a problem with event sending if user attributes have been set prior to starting taplytics.
2. New Feature: [Setting Attributes on First Launch](https://github.com/taplytics/Taplytics-Android-SDK/blob/master/START.md#user-attributes-on-first-launch)
3. New Feature: [Test Specific Experiments and Variations](https://github.com/taplytics/Taplytics-Android-SDK/blob/master/EXPERIMENTS.md#testing-specific-experiments)
4. Limit size of metadata to disallow heavy network calls.
5. Starting options to entirely disable borders during tests.
6. Upgraded build tools and support libs to most recent (23.0.3 at the time, as well as support libs 23.3.+)
7. Deleted all releases that had a bug regarding #2 in this list. If you were using that, please contact us. 

**[1.7.18](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.18)**

1. Security check fix surrounding (unused) local IPs.
2. Complex view hierarchy debug mode improvements.

**[1.7.17](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.17)**

1. Added Taplytics Session Listener.

**[1.7.16](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.16)**

1. Fixed potential listview hang.
2. Enforce button colors on Taplytics dialogs. 

**[1.7.15](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.15)**

1. Fixed some initialization errors on Chinese phones.
2. Persistent experiment caching.

**[1.7.13](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.13)**

1. Draft experiments returned in getRunningExperiments callback. 


**[1.7.12](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.12)**

1. Weakreference safety

**[1.7.11](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.11)**

1. Fix issue with push open listener

**[1.7.10](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.10)**

1. Fix support fragments issue

**[1.7.9](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.9)**

1. Handle possible type mismatch in dynamic variables
2. Use weak refs to prevent potential leaks
3. Other fixes

**[1.7.8](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.8)**

1. Add notification priority option.
2. Dont warn on socketio libs during release builds.
3. Fix dynamic variable type mismatch with booleans and strings.

**[1.7.7](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.7)**

1. Added overlayOn() and overlayOff() functions to manually handle unique youtube cases. 

**[1.7.6](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.6)**

1. Fragment change performance increase
2. First loads on fragment performance increase
3. No longer use 'getItem' anywhere for viewpagers
4. No longer block youtube due to overlays
5. ListView/Recyclerview performance tweaks


**[1.7.5](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.5)**

1. Tracking current fragment without calling getItem() or instantiateItem()
2. Build tools update
3. Consistent internal versioning

**[1.7.4](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.4)**

1. Bug fixes related to adapter views

**[1.7.3](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.3)**

1. Limited session background time to 24 hours

**[1.7.2](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.2)**

1. Fix live pairing issues

**[1.7.0](https://github.com/taplytics/Taplytics-Android-SDK/releases/tag/1.7.0)**

1. [Changed to new socket.io dependency](https://github.com/taplytics/Taplytics-Android-SDK/blob/master/SOCKETS.md)
2. Support for ImageButtons and StateDrawables. 

## Questions or Need Help

_The Taplytics team is available 24/7 to answer any questions you have. Just email support@taplytics.com or visit [our docs page](https://taplytics.com/docs?utm_source=github&utm_campaign=documentation&utm_medium=content) for more detailed installation and usage information._
