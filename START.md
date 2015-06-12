You can get started with using Taplytics on Android in minutes. Just follow the steps below:

| # | Step |
| - | ----------------- |
| 1 | Install: [Android Studio](#android-studio-installation), [Eclipse](#eclipse-installation) |
| 2 | [Initialize][#initialization] |
| 3 | Send [User Attributes](#user-attributes) (optional) |
| 4 | Send [Events](#events) (optional) |
| 5 | Setup an Experiment: [Visual](#visual-editing) or [Code-based](#code-experiments) (optional) |


## Instalation

### Android Studio Installation

1. _In your module’s build.gradle, add the url to the sdk._

	  ```
  repositories {                                                                                              
    maven { url "https://github.com/taplytics/Taplytics-Android-SDK/raw/master/AndroidStudio/" }
  }      
  ```
  
2. _In your *module’s* build.gradle dependencies (not your project's build.gradle), compile Taplytics and its dependencies._

  	```
  dependencies {                                                                   
    //Taplytics                                                                        
    compile("com.taplytics.sdk:taplytics:+@aar")  
    
    //Dependencies for taplytics
    compile("com.mcxiaoke.volley:library:+")
    compile("com.squareup.okhttp:okhttp-urlconnection:+")
    compile("com.squareup.okhttp:okhttp:+")
   
    //Excluding org.json due to compiler warnings
    //socket.io connections only made on debug devices OR if making live changes to a release build.
    //No socket.io connection will be made on your release devices unless explicitly told to do so. 
    compile("com.github.nkzawa:socket.io-client:+") {
        exclude group: 'org.json'
    }
    compile("com.github.nkzawa:engine.io-client:+") {
        exclude group: 'org.json'
    }
    
    //Only include this if you wish to enable push notifications:
    compile("com.google.android.gms:play-services-gcm:7.5.0")
  }    
  ```
  
  
3. _Override your Application’s onCreate() method (not your main activity) and call Taplytics.startTaplytics(). If you don't have an Application class, create one. It should look like this:_

	```java	  	  
  public class ExampleApplication extends Application {
    @Override
    public void onCreate() {
      super.onCreate();
      Taplytics.startTaplytics(this, "YOUR TAPLYTICS API KEY");
    }
  }
  ```
4. _Now, add the proper permissions, and the Application class to your app’s AndroidManifest.xml in the Application tag._

 	 ```xml
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  <application
    android:name=".ExampleApplication"
    ...
  ```

5. _Finally, add the following intent-filter tag to the end of your *MAIN* activity:_
	
	First, [get your Taplytics URL Scheme from your Project's Settings](https://taplytics.com/dashboard):

	![image](https://taplytics.com/assets/docs/install-sdk/url-scheme.png)
	
	Then, add it to your manifest:

	```xml
			...
	           <intent-filter>
                <action android:name="android.intent.action.VIEW"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <category android:name="android.intent.category.BROWSABLE"/>
                <data android:scheme="YOUR URL SCHEME"/>
            </intent-filter>
        </activity>
    ```


6. _Add the following to your Proguard rules:_

  
  
  (Only if using Support Fragments)

	```
  -keep class android.support.v4.app.Fragment { *; }
  -keep class android.support.v4.view.ViewPager
  -keepclassmembers class android.support.v4.view.ViewPager$LayoutParams {*;}
  ```
  
  (Only if using Mixpanel)
  
  	```
  	-keep class com.mixpanel.android.mpmetrics.MixpanelAPI { *;}
  	```
  
  (Only if using Flurry)
  
  	```
	-keep class com.flurry.android.FlurryAgent { *; }
  	```
  	
  (Only if you see gradle compiler errors with com.okio)
  ```
  	-dontwarn okio.**
	-dontwarn java.nio.file.*
	-dontwarn org.codehaus.mojo.animal_sniffer.IgnoreJRERequirement
```
  
7. _That's it! Now build and run your app, you can start creating experiments with Taplytics!_


### Eclipse Installation

1. _Download the taplytics.jar [here](https://github.com/taplytics/Taplytics-Android-SDK/raw/master/taplytics.jar)_
2. _Copy the jar into your 'libs' directory in your project._
3. _Right click the jar in Eclipse, click Build Path > add to build path_
4. **NEW:** _Add Google Play Services to your project by following the steps listed [here.](http://developer.android.com/google/play-services/setup.html) Be sure to change the dropdown to "Eclipse with ADT"_
5. _Override your application’s onCreate() method (not your main activity) and call Taplytics.startTaplytics(). It should look like this:_

	```java
  public class ExampleApplication extends Application {
    @Override
    public void onCreate() {
      super.onCreate();
      Taplytics.startTaplytics(this, "YOUR TAPLYTICS API KEY");
    }
  }
  ```
6. _Add the proper permissions, and the Application class to your app’s AndroidManifest.xml in the Application tag._

  	```xml
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  <application
    android:name=".ExampleApplication"
    ...
  ```
  
7. _Finally, add the following intent-filter tag to the end of your *MAIN* activity:_
	
	First, [get your Taplytics URL Scheme from your Project's Settings](https://taplytics.com/dashboard):

	![image](https://taplytics.com/assets/docs/install-sdk/url-scheme.png)
	
	Then, add it to your manifest:

	```xml
			...
	           <intent-filter>
                <action android:name="android.intent.action.VIEW"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <category android:name="android.intent.category.BROWSABLE"/>
                <data android:scheme="YOUR URL SCHEME"/>
            </intent-filter>
        </activity>
    ```

8. _Add the following to your Proguard rules:_
  
  (Only if using Support Fragments)

	```
  -keep class android.support.v4.app.Fragment { *; }
  -keep class android.support.v4.view.ViewPager
  -keepclassmembers class android.support.v4.view.ViewPager$LayoutParams {*;}
  ```
  
  (Only if using Mixpanel)
  
  	```
  	-keep class com.mixpanel.android.mpmetrics.MixpanelAPI { *;}
  	```
  
  (Only if using Flurry)
  
  	```
	-keep class com.flurry.android.FlurryAgent { *; }
  	```
  
  (Only if you see gradle compiler errors with com.okio or com.nio)
  ```
  	-dontwarn okio.**
	-dontwarn java.nio.file.*
	-dontwarn org.codehaus.mojo.animal_sniffer.IgnoreJRERequirement
```
  
  
9. _That's it! Now build and run your app, you can start creating experiments with Taplytics!_


## Setup

To use Taplytics and set up experiments, refer to [the Taplytics online docs.](https://taplytics.com/docs/)

To switch between experiments or variations in debug mode, select them on the website, or **shake the device ** and select which variation or experiment you wish to view.

### Initialization

Taplytics can be started with a few options to help you use it during development.

First, the base method:

```java
Taplytics.startTaplytics(this, "Your Api Key");
```

Or, add a map of options.

```java
Hashmap<String, Object> options = new Hashmap<>();
options.put("optionName",optionValue);
Taplytics.startTaplytics(this, "Your Api Key");
```

Possible options are:

| Option Name  | Values | Default | Explanation
|---|---|---|---|
|liveUpdate   | boolean: true/false  | true  | Disable live update to remove the border, and activity refreshing in your debug builds to test the functionality of your applications as if they were in release mode. Note that this functionality is always disabled in release builds.  |   
| shakeMenu | boolean: true/false   | true  | In your debug builds, disable the quick menu that appears when you shake your device. This menu is never present in release builds.|   

#### The Border / Shake menu. 

When connected to an experiment on a **debug** build, a border will show around your app window. This shows which experiment and variation you are currently viewing.

You can long-press on the top of the border to switch experiments, or shake your device and pick from the menu, or select an experiment from the Taplytics website.

**The border and shake menu will _NOT_ appear on release builds.**

### User Attributes

Its possible to send custom user attributes to Taplytics using a JSONObject of user info. 

The main possible fields are:

|Parameter  |Type         |
|---      |---          |
|email      | String    |
|user_id    | String    |
|firstname  | String    |
|lastname   | String    |
|name     | String    |
|age      | Number    |
|gender     | String    |

You can also add anything else you would like to this JSONObject and it will also be passed to Taplytics. 

An example with custom data: 

```java
JSONObject attributes = new JSONObject();
attributes.put("email", "johnDoe@taplytics.com");
attributes.put("name", "John Doe");
attributes.put("age", 25);
attributes.put("gender", "male");
attributes.put("avatarUrl", "https://someurl.com/someavatar.png");

attributes.put("someCustomAttribute",50);
attributes.put("paidSubscriber", true);
attributes.put("subscriptionPlan", "yearly");

Taplytics.setUserAttributes(attributes);
```

### Code Experiments

####Setup

To set up a code experiment in Taplytics, please refer to the [Taplytics code-based experiment docs](https://taplytics.com/docs/code-experiments).

####Usage

Taplytics automatically generates the base needed for your code experiment. Paste it into the relevant section of your app, and apply the variables as necessary. 

It is suggested that you place the code calling the experiment in its own function (as opposed to an oncreate).

For example:

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  setContentView(some_layout);
  
  // Run this code experiment. This triggers the experiment.
  runAnExperiment();
}
```
  
Then, in that function, add your experiment code generated by Taplytics, and modify it as you need.
  
```java
private void runAnExperiment(){
  Taplytics.runCodeExperiment("experiment name", new TaplyticsCodeExperimentListener() {
  
    @Override
    public void baselineVariation(Map<String, Object> variables) {
        
            // Insert baseline variation code here.
            Object myVar0 = variables.get("foo"); // can be null if no experiment is found
          }
          
    @Override
    public void experimentVariation(String variationName, Map<String, Object> variables) {
          Object myVar0 = variables.get("foo"); // can be null if no experiment is found
        
          if (variationName.equals("Variation 1")) {
            // Insert Variation 1 variation code here.
          } else if (variationName.equals("Variation 2")) {
        // Insert Variation 2 variation code here.
      }
    }
  
    @Override
    public void experimentUpdated() {
      // Use this method to re-run your code experiments when testing your ex periment variations.
    }
  });
}
```

This separate function is suggested, because if you would like to update experiments instantly for debug testing or another reason, you can simply place the `runAnExperiment()` function into the `experimentUpdated()` block.

### Visual Editing

You don't have to do anything else! All visual editing is done on the Taplytics dashboard. See the docs on visual editing [here](https://taplytics.com/docs/visual-experiments).


### Events

####Automatic Events

Some events are automatically tracked by Taplytics and will appear on your dashboard. These events are:

* App Start
* Activity and/or Fragment load
* Activity and/or Fragment destroy
* Activity pause
* App background
* Viewpager changes

App terminate is also tracked, but this is only true when your MAIN activity is at the bottom of your activity stack, and the user exits the app from that activity.

No changes are needed in your code for this event tracking to occur. 

####Custom Events

To log your own events, simply call:    

```java
Taplytics.logEvent("Your Event Name");
```

You can also log events with numerical values:

```java
Number num = 0;
Taplytics.logEvent("Your Event Name", num);
```
  
And with custom object data:

```java
Number num = 0;
JSONObject customInfo = new JSONObject();
customInfo.put("some title",someValue)
Taplytics.logEvent("Your Event Name", num, customInfo);
```

####Revenue Logging

Its also possible to log revenue.

Revenue logging is the exact same as event logging, only call `logRevenue`:

```java
Number someRevenue = 10000000;  
Taplytics.logRevenue("Revenue Name", someRevenue);
```
  
And similarly, with custom object data:

```java 
Number someRevenue = 10000000;
JSONObject customInfo = new JSONObject();
customInfo.put("some rag",someValue)
  
Taplytics.logRevenue("Revenue Name", someRevenue, customInfo);
```

####External Analytics
At the moment, Taplytics supports both Mixpanel and Google Analytics as a source of external analytics.

#####Mixpanel

When the Taplytics SDK is installed alongside Mixpanel, all of your existing and future Mixpanel analytics will be sent to both Mixpanel _and_ Taplytics.

#####Google Analytics 7.0.0-

If you are using Google Analytics 7.0.0 and below, all Google Analytics will automatically be sent to both Google Analytics _and_ Taplytics.

#####Google Analytics 7.3.0+

If you are using Google Analytics 7.3.0 or above, you have the option of changing things a bit to send your Google Analytics to both Google _and_ Taplytics.

Simply find all instances of `tracker.send(new Hitbuilder...)` and replace them with `Taplytics.logGAEvent(tracker, new Hitbuilder...)`

This can be done with a simple find/replace in your application.

An example:

```java
Tracker t = TrackerManager.getInstance().getGoogleAnalyticsTracker(TrackerManager.TrackerName.APP_TRACKER, getApplication());
t.send(new HitBuilders.EventBuilder().setCategory("someCategry").setAction("someAction").setLabel("someLabel").setValue(12).build());
```

Would be changed to:

```java
Tracker t = TrackerManager.getInstance().getGoogleAnalyticsTracker(TrackerManager.TrackerName.APP_TRACKER, getApplication());
Taplytics.logGAEvent(t, new HitBuilders.EventBuilder().setCategory("someCategry").setAction("someAction").setLabel("someLabel").setValue(12).build());
```

### Delay Load

Much like the iOS SDK, Taplytics now has the option to delay the loading of your main activity while Taplytics gets initial view changes ready. Keep in mind that this initial load will only take a while the very first time, after that, these changes will be saved to disk and will not need a delay thereafter.

There are two methods to do this, **use both at the start of your oncreate after ```java setContentView()```**:

####Delay Load With Image
In this instance, Taplytics takes care of the loading for you. Taplytics creates a splash screen with the provided image. The image will fade automatically after the given time, or when Taplytics has successfully loaded visual changes on the provided activity.

Method: ```Taplytics.delayLoad(Activity activity, Drawable image, int maxTime) ```

**Activity**: the activity (typically main activity) that will be covered in a splash image.

**Image**: A Drawable image that will be the splash screen.

**Max Time**:  Regardless of the results of Taplytics, the image will fade after this time. Milliseconds.

**Example**:

```java
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main_layout);

        Taplytics.delayLoad(this, getResources().getDrawable(R.drawable.image5), 2000);
        ...
```

####Delay Load with Callbacks
In this instance, Taplytics provides callbacks when the delay load should begin, and when the delay load ends. The callback will also return after the provided timeout time has been reached. This provides you the ability to show a splashscreen that is more than just a simple image. 

Method: ```Taplytics.delayLoad(int maxTime, TaplyticsDelayLoadListener listener) ```


**Max Time**: Regardless of the results of Taplytics, the image will fade after this time. Milliseconds.

**Listener**: This listener will provide the necessary callbacks.

**Example**:

```java

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main_layout);

        Taplytics.delayLoad(2000, new TaplyticsDelayLoadListener() {
            @Override
            public void startDelay() {
                //Start delaying!
            }

            @Override
            public void delayComplete() {
                //Loading completed, or the given time has been reached. Insert your code here.
            }
        });
        ...
        
```


### Advanced Device Pairing

Link a device (even in release mode) to Taplytics.

**NOTE: This is used only for deeplink pairing, and is unnecessary if your main activity does NOT have a singleTask flag.**

Retrieve deeplink through Taplytics deeplink intercepted via either email or SMS device pairing. It contains your Taplytics URL scheme and device token. If you wish to intercept the deeplink and then pair the device yourself in your application's code, call this method, like so:

```java
private void handleDeepLink(Intent intent) {
  String tlDeeplink = intent.getDataString(); //example deep link: 'tl-506f596f://e10651f9ef6b'
  if (tlDeeplink == null) {
      // No deeplink found
      return;
  }
  Taplytics.deviceLink(tlDeeplink);
}
```