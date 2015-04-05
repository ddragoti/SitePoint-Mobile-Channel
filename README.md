Firstly read [SitePoint's general writers guidelines](http://www.sitepoint.com/writing-guidelines/), the following is a set of specific set of guidelines just for the mobile channel.

_Are you back? Great!_

## Language

### I vs We
You are writing the article, so use 'I', not 'We'. If you are mentioning SitePoint, then use 'We', or better, 'SitePoint'.

### You, Your, The, They, It
I'm not a big fan of 'your' as in "Add this to your code". I prefer the use of "the", so "Add this to the code". If you need to refer to a person, don't use a gender, use "they".

### Common 'gotchas'
SitePoint writers are an international bunch of people, so the level of written English varies. That's fine, but here is a list of common mistakes I find in articles submitted by non-native speakers to learn from and avoid.

* On, In, Into

## Images

Images for article should be upload to SitePoint's CDN, if you are an existing author, this will be a new process for you. I don't have access to your passwords, so visit [sitepoint.com/wp-login.php](https://www.sitepoint.com/wp-login.php) and click 'Lost your password?' to reset it, your username will be _FirstnameLastname_ or your email address.

Once logged in, open _Media -> Add New_ and upload your media. Sometimes the uploader gets stuck at the 'crunching' stage, your image will still be uploaded.

Find your image in the _Media -> Library_ tab, click it to get the url and use that url in your markdown files.

## Code
Code is one of the elements of an article that our readers will enjoy most and pay most attention to. Therefore there are several points we need to pay careful attention to:

Unless you are just presenting code concepts, every tutorial should have an associated GitHub repository that is mentioned in the tutorial.

Code should be explained, not just presented as a block. Mention where the code should go, in what file and after what exisiting code. Readers should be able to follow the tutorial without knowing what you're thinking, don't assume they do or should.

If there are any extra steps required to get your code working such as utilising external libraries, then make sure these are mentioned.

In short, "It works on my machine" is not an accaptible response. If you have any special build systems, or lots of plugins installed on your computer, this doesnt mean a reader will. I will generally spend about half an hour figuring out why code wont work on my computer before asking you take a look, readers wont.

### Special notes for iOS
All code should be compilable, runnable and work in teh latest version of Xcode, (at time of writing 6.2) and iOS (At time of writing 8.2). It should run and be usable on the latest available iPhone / iPad.

### Special notes for Android
The nature of Android means that there are many different IDEs, SDKs and device configurations, so here are the guidelines that all code submissions should conform to:

* All code should be openable, compilable and runnable in [Android Studio](http://developer.android.com/tools/studio/index.html) as this is now the official Android IDE.
* All code should be built to compile and run under the current API version and the two prior to it. So at time of wrtiign these are 19, 21 and 22. If you are creating specialised Android applications (such as for Android Wear), the same applies, but I will assume you know what you're doing.
* All code should be usable on a Nexus 5, the current Android reference device (in my opinion). This is the default emulator, so you don't need a rel device to test this.

## Author Interaction
Writing and submitting articles is only one part of what SitePoint is about, we are also a community. It is not compulsory to comment on your articles, or get involved in our forums, but it's encouraged! Writers who engage more with our community are more likely to have their submissions chosen and your artciles are likely to have more readers. (That's not a bribe by the way.)

## Submission process
