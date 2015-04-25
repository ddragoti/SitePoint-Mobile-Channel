Introduction to Android Accessibility
=========================

Everybody agrees that an app should be easy to use, intuitive and user friendly, but is it really enough? We often forget that an important part of app development is making sure your app is accessible to everyone and at the same time easy to navigate even for people with visual or physical disabilities. 

Android offers a lot in term of accessibility options and features but those often get neglected during the design and implementation phase. Accessibility APIs were first introduced in Android 1.6(API level 4) but still to this day many developers are not very familiar or interested in them. Accessibility has always been an after-thought and if you make a quick search on Google or StackOverflow very few mentions pop up. But it shouldn't be like this, because implementing accessibility features into your app is fairly easy and straightforward, so today we are going to take a look at how to implement basic accessibility features into your app. 

Adding a textual description to UI elements
---------------------------------------------

Every designer worth of his salt knows that a well designed interface should be self-explanatory and intuitive without the need of help manuals to navigate, but this is not always the case.
Physically impaired users necessitate of audio hints and/or visual cues to navigate even the simplest of interfaces so this is why we need **Content Descriptions**.

Content Descriptions are the easiest accessibility feature to implement and one of the most useful. They are like the comments in your code. Although, Google generally advises using descriptions mainly for ImageView, ImageButton and CheckBox elements as this is where they are most needed, at the end of the day it is up to the app developer to decide.

You can add descriptions in two ways: via xml layout or traditional Java methods.
So let’s get right to it, using xml you can add a description to an image like this(note the last line):

    <ImageView
    	android:id=”@+id/new_image”
    	…
    	...
    	android:contentdescription=”@string/image_desc”
    	/>



`@string` is declared in the strings.xml file like this:

    <string name="image_desc">Simple description of what the image represents</string>

However, for `EditText` fields you should use the line below to explain to the user what they should type:

    android:hint = "Name Field"


Also, if your interface elements change the state like a toggle button or list item checkboxes you should ensure that the contentDescription changes dynamically depending on the element state.
In these cases you better be using the `setContentDescription()` method:

  
 

      label.setContentDescription("Toggle is set to: " +  (ToggleButton).isChecked())

  

As we mentioned above, don’t add a description if it is not necessary, because you may annoy your users. If you feel the element is self explanatory and does not have any real function, for example an app icon use this:

    android:contentdescription=”@null”

Navigation without using the touchscreen
-----------------------------------------------------

Also called focus navigation it means that users can use your app without the need for a touchscreen but instead using only directional controllers. These include D-pads, trackballs, gestures, arrow keys or just their eyes like on some modern smartphones. It’s very important that your app supports these different mechanisms for navigation.


Firstly you need to make sure that every input element is focus-able and clickable using the directional buttons. Also, do not forget to visually indicate the element that the user is focusing on by highlighting it. Every control element in Android has this feature on by default but if you have created your own elements, make sure to make them focus-able using the `setFocusable(true)` method or the `android:focusable` attribute like this:

    <EditText
            ...
           android:focusable = "true"
      />



Additionally,  Android has its own algorithms for finding the nearest focusable element so users can navigate the interface intuitively with the directional controller, but if in any case you want to override those features use the xml attributes below:

> android:nextFocusDown,  
> android:nextFocusLeft, 
> android:nextFocusRight,  
> android:nextFocusUp

These are self-explanatory but to give you a good idea how to use them check this code sample:

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


Creating your own Accessibility Service
---------------------------------------------

An accessibility service is used to communicate with the user on behalf of the application and provide navigational feedback like haptic feedback, text to speech and visual cues. Android provides such services like TalkBack, Explore by touch and others by default. These help assisting users who are unable to interact with the device normally because of physical disabilities or in special situations like driving, exercising etc.

You can create your own accessibility services as part of your main application and bundle them together or like a standalone app. For more information regarding this topic, check out the [official documentation](http://developer.android.com/training/accessibility/service.html).


Accessibility testing
------------------------

Testing is as important as the implementation part, so make sure to thoroughly test your apps after you implement the accessibility features by enabling TalkBack and Explore by touch and trying to navigate your app using only the audio feedback and directional controls.
Be sure to check that every control element provides the necessary feedback and the audio prompt are not repetitive and longer than needed. In addition, the Android Design guidelines suggests that every focus-able element should be at least 48dp in length and width so this also should be a concern.

To support users with hearing disabilities be sure to accompany audio feedback with another secondary mechanism like haptic feedback or visual cues like pop ups and notifications.
Also, if your app provides video playback make sure to offer subtitles or captions support.


Conclusion
--------------

In summary, we learned why accessibility should be an important part of your development timeline and how to implement different features into your app. Every developer should focus on making their apps accessible by everyone regardless of how they interact with the device.
But I want to hear from you now. Do you use any of these features in your apps? Do you often test your apps for accessibility? Tell us below.
