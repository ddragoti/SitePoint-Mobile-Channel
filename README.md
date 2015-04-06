Firstly read [SitePoint's general writers guidelines](http://www.sitepoint.com/writing-guidelines/), the following is a set of specific set of guidelines just for the mobile channel.

_Are you back? Great!_

## Language

### I vs We
You are writing the article, so use 'I', not 'We'. If you are mentioning SitePoint, then use 'We', or better, 'SitePoint'.

### You, Your, The, They, It
I'm not a big fan of 'your' as in "Add this to your code". I prefer the use of "the", so "Add this to the code". If you need to refer to a person, don't use a gender, use "they".

### Common 'gotchas'
SitePoint writers are an international bunch of people, so the level of written English varies. That's fine, but here is a list of common mistakes I find in articles submitted by non-native speakers to learn from and avoid.

* The word 'also' is overused, you can probably just remove it.

## Images

Images for article should be upload to SitePoint's CDN, if you are an existing author, this will be a new process for you. I don't have access to your passwords, so visit [sitepoint.com/wp-login.php](https://www.sitepoint.com/wp-login.php) and click 'Lost your password?' to reset it, your username will be _FirstnameLastname_ or your email address.

Once logged in, open _Media -> Add New_ and upload your media. Sometimes the uploader gets stuck at the 'crunching' stage, your image will still be uploaded.

Find your image in the _Media -> Library_ tab, click it to get the url and use that url in your markdown files.

## Code
Code is one of the elements of an article that our readers will enjoy most and pay most attention to. Therefore there are several points we need to pay careful attention to:

Unless you are just presenting code concepts, every tutorial should have an associated GitHub repository that is mentioned in the tutorial.

Code should be explained, not just presented as a block. Mention where the code should go, in what file and after what existing code. Readers should be able to follow the tutorial without knowing what you're thinking, don't assume they do or should.

If there are any extra steps required to get your code working such as utilising external libraries, then make sure these are mentioned.

In short, "It works on my machine" is not an acceptable response. If you have any special build systems, or lots of plugins installed on your computer, this doesnt mean a reader will. I will generally spend about half an hour figuring out why code wont work on my computer before asking you take a look, readers wont.

### Special notes for iOS
All code should be compilable, runnable and work in the latest version of Xcode, (at time of writing 6.2) and iOS (At time of writing 8.2). It should run and be usable on the latest available iPhone / iPad.

### Special notes for Android
The nature of Android means that there are many different IDEs, SDKs and device configurations, so here are the guidelines that all code submissions should conform to:

* All code should be openable, compilable and runnable in [Android Studio](http://developer.android.com/tools/studio/index.html) as this is now the official Android IDE.
* All code should be built to compile and run under the current API version and the two prior to it. So at time of writing these are 19, 21 and 22. If you are creating specialized Android applications (such as for Android Wear), the same applies, but I will assume you know what you're doing.
* All code should be usable on a Nexus 5, the current Android reference device (in my opinion). This is the default emulator, so you don't need a real device to test this.

## Author Interaction
Writing and submitting articles is only one part of what SitePoint is about, we are also a community. It is not compulsory to comment on your articles, or get involved in our forums, but it's encouraged! Writers who engage more with our community are more likely to have their submissions chosen and your articles are likely to have more readers. (That's not a bribe by the way.)

## Submission process
If you are an existing writer, the submission process for articles has changed to allow for a more collaborative process to facilitate feedback and let us all learn from each other. This process and set-up has been [heavily borrowed from our PHP editor](https://github.com/sitepoint-editors/php-peers).

### Pre-Writing
1. Submit an idea on the channel's [Trello board](https://trello.com/b/HxaTeMXt/sitepoint-mobile-channel) into the 'Topic Suggestions' column.
2. We will discuss the topic on the Trello card.
3. Please don't start a topic until it has been accepted, otherwise you may waste your time on writing something that wont be published.

### Article Finished
1. If you don't have a GitHub account then create one. If you're not sure how to do this, [then let me know](mailto:chris.ward@sitepoint.com) and I'll explain what it is and how it works.
2. [Fork this repository](https://help.github.com/articles/fork-a-repo/) to create a local copy. If you already have a fork, [make sure it's in sync](https://help.github.com/articles/syncing-a-fork/).
3. Create a branch for each article you write and add your article using this folder structure: _YourName -> ArticleName.md_.
4. When you're finished, [submit a pull request](https://help.github.com/articles/using-pull-requests/).

Once you have submitted a pull request we will discuss the further editing of articles in GitHub. This allows for identifying and commenting specifically on particular parts of articles and for us to track teh changes to an article over time. This may seem an over the top way of managing article submissions, but it lets you see exactly where problems are, what has changed and you can ask why. It also allows for a very easy transition to the SitePoint website, which may be more automated in the future.

## The Future
This is a new process, there will be some initial problems that we all encounter along the way. However, over time it will stabilize, improve and more functionality will be added to make things easier for everyone… Watch this space!
