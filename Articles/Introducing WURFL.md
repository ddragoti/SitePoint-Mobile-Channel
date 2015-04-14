##Introducing wurfl.js - a simple device detection repository

 The ability to design responsive web pages is a skill sought by many developers. Free online tools have enabled designers to get up to speed in what they need to know and how to create such pages.

But not so long ago, web designers had to make use of User-Agent strings embedded in HTTP headers. Usually you only knew if the device used was an iPhone, Android or Desktop computer, no other information. This was a tiring, tedious practice and explains why responsive design has become so popular. Responsive enables developers to create a website that cater to every device and screen size without having to deal with the complexities of server side programming.

However, there are some instances when a developer may need to know what kind of device is accessing their website. This is where WURFL-(Wireless Universal Resource FiLe) comes in handy.

#What is WURFL
WURFL is a rowing list of set of proprietary APIs and an XML configuration file which contains information about device capabilities and features for a variety of mobile devices. This provides developers with valuable information about the type of devices their clients are using to access their website.

The purpose behind WURFL is to enable developers to present content nicely and provide a better experience for the users, while at the same time giving developers insight about the users behaviors and usage patterns. It tries to do this in a fast, easy implementable and cost-free way.

Want to learn to use WURFL yourself? Let's get our hands dirty.

Firstly you need to add this line of Javascript to your page:

><script type='text/javascript' src="//wurfl.io/wurfl.js"></script>

In doing so you essentially just imported a JS file and that enables you to access the WURFL object in JavaScript, which looks like this:

>{
>  complete_device_name:"Google Nexus 4",
>  form_factor:"Smartphone",
>  is_mobile:true
>}


I quickly set up an example page [here](http://ddragoti.github.io/WURFL/), so you can see it in action.
The source code is hosted on github and you can have a look at it [here](https://github.com/ddragoti/WURFL/blob/gh-pages/index.html) .

You probably noticed that there are only three properties there:

*complete_device_name which gives you the make and model of the device accessing your website. (However, if the device is a desktop computer it will give you a generic “desktop computer” response).

*form_factor which can be any of these:
desktop, app, tablet, smartphone, feature phone, other mobile etc.

*is_mobile is a boolean function which can be either true or false depending on the device, if it is a mobile or tablet it will return true.

These properties enable you to do things like:

>if(!WURFL.is_mobile){
>
>      $('#wurfl .is-mobile span').html("false");
>}



#Advertising

WURFL can also help you in stratetically displayed advertising. Some ads look better on mobile devices and others are more appropriate for desktops or laptops. WURFL can help you control how ads get displayed and on what kind of devices.
You can simply control the ads by using *WURFL.is_mobile* feature, or if you want to have more control, use the *form_factor* option and target ads depending on the type of device.

#WURFL and Modernizr

Even though what WURFL offers may similar to what can be achieved with Modernizr, they're not the same. They’re not even in the same category of services. Modernizr gives you information about the capabilities of the web browser, whereas WURFL provides insight about the hardware. And there are instances where knowing the device’s make and model  is better than knowing only the browser capabilities of the device because even though the browser may support a certain feature, the actual device may not. However, this doesn't mean that you should get rid of Modernizr altogether. Using WURFL and Modernizr together will give you greater control over the way your websites work and look in any kind of device. A good example is the CSS capabilities of Modernizr, which enables you to use different styles depending on the device. This great feature is available on WURFL too and you need a single line of Javascript for it to work:

>document.documentElement.className += ' ' + (WURFL.is_mobile ? '' : 'no-') + "mobile";

In this simple case, when a device is mobile the html tag will be assigned the “is_mobile” class, otherwise the class will be equal to “no-is_mobile”.
By including this you can create different style sheets depending on the class assigned.

#Conclusion

For someone who knows how tricky it is to get information about the different devices accessing your service and have used Device Description Repositories that required server-side libraries before, WURFL is a great and simple service and at no cost whatsoever.

It can enable developers control over how their content gets presented on a multitude of devices, better targeting of advertising and better analytics over the way their users access their websites.
