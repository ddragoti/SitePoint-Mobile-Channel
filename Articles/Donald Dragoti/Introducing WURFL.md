Device detection for your Apps with WURFL.js
--------------------------------------------

Responsive web design is not a new topic to mobile developers, many of us are well versed in the process and best practice guidelines. One of these best practices is displaying page elements in different ways based on the browser or device capabilities of the user. To accomplish this designers have traditionally made use of `User-Agent` strings embedded in HTTP headers. These would generally only tell you if the device used was an iPhone, Android or Desktop computer, no other information.

There are many occasions when a developer needs to know more detail than this to create a fully responsive design. This is where WURFL.js (Wireless Universal Resource File) can help.

What is WURFL.js?
=================

WURFL.js is a growing list of set of proprietary APIs and a XML configuration file which contains information about device capabilities and features for a variety of mobile devices. This provides developers with valuable information about the type of devices their clients are using to access their website. It leverages the same power of Server-side detection that you may be familiar with (using server side languages) without you needing to set any of that up.

The purpose behind WURFL.js is to enable developers to opimise the rpesentation of content and provide a better user experience, whilst also giving developers insight about users behaviors and usage patterns. It tries to do this in a fast, easy implementable and cost-free way.

How do you use WURFL.js? Let's get our hands dirty.

Firstly add this line of Javascript to your page:

```
<script type='text/javascript' src="//wurfl.io/wurfl.js"></script>
```

Here we have imported a JavaScript file that enables us to access the WURFL object in JavaScript. For example:

```
{ complete_device_name:"Google Nexus 4", form_factor:"Smartphone", is_mobile:true }
```

I have set up an example page [here](http://ddragoti.github.io/WURFL/), so you can see WURFL.js in action. The source code can be found on github [here](https://github.com/sitepoint-editors/WURFL) .

Notice that there are only three properties used:

-	`complete_device_name` which gives the make and model of the device accessing your website. (However, if the device is a desktop computer it will give you a generic “desktop computer” response).

-	`form_factor` which can be any one of: desktop, app, tablet, smartphone, feature phone, other mobile etc.

-	`is_mobile` is a boolean which can be either true or false depending on the device. If it is a mobile or tablet it will return true.

These properties enable you to do things like:

```
if(!WURFL.is_mobile) {

  $('#wurfl .is-mobile span').html("false");

}
```

Advertising
-----------

WURFL.js can help you strategically display advertising. Some ads look better on mobile devices and others are more appropriate for desktops or laptops. WURFL.js can help you control how ads get displayed and on what kind of devices. You can control the ads by using the `WURFL.is_mobile` feature, or if you want to have more control, use the `form_factor` option and target ads depending on the type of device.

WURFL.js and Modernizr
----------------------

Although what WURFL.js offers is similar to what can be achieved with Modernizr, they're not the same. Modernizr gives information about the capabilities of the web browser, whereas WURFL.js provides insight about the hardware. There are instances where knowing the device’s make and model is better than knowing only the browser capabilities of the device because whilst the browser may support a certain feature, the device may not. This doesn't mean that you should get rid of Modernizr altogether. Using WURFL.js and Modernizr together will give you greater control over the way your websites work and look on any kind of device. A good example is the CSS capabilities of Modernizr, which enables you to use different styles depending on the device. This feature is available in WURFL.js too and requires just a single line of Javascript to work:

`document.documentElement.className += ' ' + (WURFL.is_mobile ? '' : 'no-') + "mobile";`

In this simple example, when a device is mobile the `HTML` tag will be assigned the `is_mobile` class, otherwise the class will be equal to `no-is_mobile`. By including this you can create different style sheets depending on the class assigned.

Conclusion
----------

I know how tricky it is to get information about different devices accessing your application and have used Device Description Repositories before that required server-side libraries. To me WURFL.js is a great and simple resource, especially for no cost.

It can give developers control over how their content gets presented on a multitude of devices, better targeting of advertising and better analytics over the way users access their websites. Have you had any experience with WURFL?
