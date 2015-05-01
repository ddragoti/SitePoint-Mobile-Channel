# Introduction to Android Accessibility
Everybody agrees that an app should be easy to use, intuitive and user friendly, but is that enough? We often forget that an important part of app development is making sure your app is accessible and easy to navigate for everyone, even those with visual or physical disabilities.

Android offers a lot of accessibility options and features but they are often neglected during the design and implementation phase. Accessibility APIs were first introduced in Android 1.6 (API level 4) but many developers are not familiar or interested in them. Accessibility has often been an after-thought and if you make a quick search on Google or StackOverflow, there are few mentions.

It shouldn't be this way, because implementing accessibility features into your app is easy and straightforward, so today we are going to take a look at how.

## Adding a textual description to UI elements
Every good designer knows that a well designed interface should be self-explanatory and intuitive without needing instructions. But this is not always the case. Physically impaired users need audio hints and/or visual cues to navigate even the simplest of interfaces and this is where **Content Descriptions** are utilized.

Content Descriptions are the easiest accessibility feature to implement and one of the most useful. They are like the comments in your code. Google advises using descriptions mainly for `ImageView`, `ImageButton` and `CheckBox` elements as this is where they are most needed.

Descriptions are added in two ways, via XML layout or traditional Java methods.

Using XML you add a description to an image like this (note the last line):

```
<ImageView
    android:id=”@+id/new_image”
    ...
    android:contentdescription=”@string/image_desc”
    />
```

The `@string` is declared in the _strings.xml_ file like this:

```
<string name="image_desc">Simple description of what the image represents</string>
```

For `EditText` fields use the line below to explain to the user what they should type:

```
android:hint = "Name Field"
```

If your interface elements change state, like a toggle button or checkbox, you should ensure that the `contentDescription` changes dynamically depending on the state. In this case use the `setContentDescription()` method:

```
  label.setContentDescription("Toggle is set to: " +  (ToggleButton).isChecked())
```

As mentioned, don't add a description if not necessary, because you may annoy users. If you feel the element is self explanatory and does not have any real function, for example an app icon, use:

```
android:contentdescription=”@null”
```

## Navigation without using the touchscreen
Also known as focus navigation, this allows users to use your app without the need for a touchscreen but using directional controllers. These include D-pads, trackballs, gestures, arrow keys or their eyes on some modern smartphones. It's important that your app supports these different mechanisms for navigation.

Ensure that every input element is focusable and clickable using directional buttons. Don't forget to visually indicate the element that the user is focusing on by highlighting it. Every control element in Android has this feature enabled by default, but if you have created your own elements, make them focusable using the `setFocusable(true)` method or the `android:focusable` attribute:

```
<EditText
        ...
       android:focusable = "true"
  />
```

Android has algorithms for finding the nearest focusable element so users can navigate the interface intuitively with the directional controller. If you want to override this feature, use the XML attributes below:

```
android:nextFocusDown,
android:nextFocusLeft,
android:nextFocusRight,
android:nextFocusUp
```

These are self-explanatory but the following code sample demonstrates their usage:

```
 <EditText
       android:id = “@+id/upper_text_field”
        …
        ...
       android:nextFocusDown = "@+id/lower_text_field"
  />

<EditText
       android:id = “@+id/lower_text_field”
        …
        ...
       android:nextFocusUp = "@+id/upper_text_field
  />
```

## Creating your own Accessibility Service
An accessibility service communicates with a user on behalf of the application and provides navigational feedback like haptic feedback, text to speech and visual cues. Android by default provides services like TalkBack and Explore by touch. These help users who are unable to interact with the device normally because of physical disabilities or in special situations like driving, exercising etc.

You can create your own accessibility services as part of your main application and bundle them together or as a standalone app. For more information on this topic, read the [official documentation](http://developer.android.com/training/accessibility/service.html).

## Accessibility testing
Testing is as important as implementation, so make sure to thoroughly test your apps after implementing any accessibility features. This can be done by enabling TalkBack and Explore by touch and trying to navigate your app using only audio feedback and directional controls. Ensure that every control element provides the necessary feedback and that audio prompts are not repetitive and longer than needed. Additionally, the Android Design guidelines suggests that every focusable element should be at least 48dp in length and width.

To support users with hearing disabilities, accompany audio feedback with a secondary mechanism like haptic feedback or visual cues such as pop ups and notifications. If your app provides video playback, offer subtitles or caption support.

## Conclusion
We have learned why accessibility should be an important part of your development timeline and how to implement different features into an Android app. Every developer should focus on making their apps accessible by everyone regardless of how they interact with the device.

I want to hear from you. Do you use any of these features in your apps? Do you often test your apps for accessibility? Let me know in the comments below.
