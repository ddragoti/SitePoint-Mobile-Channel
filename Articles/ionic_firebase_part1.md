Bucket lists have grown in popularity since the release of the film [The Bucket List](http://www.imdb.com/title/tt0825232/) starring Morgan Freeman and Jack Nicholson. In response, app developers have been creating apps which enable users to make their own 'bucket lists'- a list of things they wish to experience before they die. In Part One of this two part  tutorial, we'll create  the framework for a simple Bucket List application using the IONIC framework. This will enable you to create a home page which will users to sign up to the Bucket list app and sign in. We'll use [Firebase](https://www.firebase.com/) as back end for our Bucket List application. Part two will show you how to create a platform for a wish list in the Bucket list app. 

[IONIC](http://ionicframework.com/) is a HTML5 mobile application development framework which helps developers build native looking apps. It is mainly focused on creating a nice looking UI using web technologies such as HTML, CSS and JavaScript. It requires JavaScript framework and AngularJS to drive it's many features like gestures and animations.

Source code from this tutorial is available on [GitHub](https://github.com/jay3dec/iBucketListApp_Part1).

## Getting Started
We'll start by installing [Node.js](https://nodejs.org/) in our system.
```
sudo apt-get install nodejs
```
Once node has been installed, install the node package manager `npm`.
```
sudo apt-get install npm
```
Use npm to install IONIC.
```
npm install -g cordova ionic
```
We'll be creating the app for Android platform. So, make sure you have the required platform dependencies installed.
Once done with the installation, create an IONIC project. 
```
ionic start iBucketApp blank
```
The above command would create a blank IONIC project. Now navigate to the project directory `iBucketApp`, add the required platform, build and emulate.
```
cd iBucketApp
ionic platform add android
ionic build android
ionic emulate android
```
If all goes well, you should be able to see the blank app running in the android emulator.

![IONIC Blank App](https://lh6.googleusercontent.com/qBoiXBVxgC_tS8lNQVgjAN47UPzJpP8DvMZMUKw8Cbk=w331-h567-no)

## Project Structure
If you have a look at the project structure, you can see that inside the project directory `iBucketApp`, there is a folder called `www`. Now `www` is the folder where we'll be working.

![Project Folder Structure](https://lh4.googleusercontent.com/-Q1VqhhdnnqA/VSkVZcmj1QI/AAAAAAAABDU/MFrqRy0hscU/w756-h567-no/8d8j8d8u.png)

As you can see, inside `www/js` there is a file called `app.js` which is the root file of our app. We'll define our application routes inside `app.js`. Inside `index.html`, we'll define the `ion-nav-view` where we'll render different templates.

Making edits and running the app on the emulator is a time consuming task. So we'll use the browser to test our app and when it's ready, we'll try it on the android emulator. To make it work with the browser we'll need to install the required `package.json` dependencies using `npm`. So inside the iBucketApp directory, run the following command to install dependencies.
```
npm install
``` 
IONIC provides command line utilities to make app development and testing easier. Once such command is `ionic serve`. Once dependencies are installed, run `ionic serve` and you should able to view the app in the web browser.

![IONIC Blank Starter App](https://lh6.googleusercontent.com/-FoVHOh9mgEo/VSkZMAgQJaI/AAAAAAAABDo/oGxL38tAou0/w741-h567-no/as8a8s7a87s.png)

## Creating Home Screen
Let's start by creating a home page for iBucketList app. Inside the `www` directory create a folder called `templates`. Inside templates, create a file called `home.html`. 

Now, we'll be switching our view as per the url requested. So, we'll make use of the IONIC directive API [ion-nav-view](http://ionicframework.com/docs/api/directive/ionNavView/). 

Remove all the code from the `index.html` body tag. Add the `ion-nav-view` directive to the body of `index.html`.
```
<body>           
  <ion-nav-view></ion-nav-view>
</body>
```
As per the url requested, we'll render different views inside the `ion-nav-view` in `index.html`. 
[ion-view](http://ionicframework.com/docs/api/directive/ionView/) is another IONIC directive API which is the child of `ion-nav-view`.  It's a container which holds the view content. Now, open `templates/home.html` and add a ion-view with a header tag.
```
<ion-view>
     <h1>This is Home Template</h1>
</ion-view>
``` 
The template and containers are ready. Now we need to define the routes and their respective views. We'll make use of [angular-ui-router](https://github.com/angular-ui/ui-router). So, open up `js/app.js` and define the`home` state.
```
.config(function($stateProvider, $urlRouterProvider) {
    $stateProvider
        .state('home', {
            url: '/home',
            templateUrl: 'templates/home.html',
            controller: 'HomeCtrl'
        })

    $urlRouterProvider.otherwise('/home');
});

```
As seen in the above code, we have defined template and controller for the url `/home`. We have also set the default url to `/home`. 
Create a file called `js/controller.js` and define the `HomeCtrl` inside it.
```
angular.module('starter.controllers', [])

.controller('HomeCtrl', ['$scope', function($scope) {


}]);
``` 
Include the `js/controller.js` file as reference in `index.html`.
```
<script src="js/app.js"></script>
<script src="js/controller.js"></script>
```
Inject `starter.controllers` in the starter app in `app.js`.
```
angular.module('starter', ['ionic','starter.controllers'])
```
Save the above changes and you should be able to see the changes in the browser.

![Home Page View](https://lh3.googleusercontent.com/--epzSKEdPOU/VSkgLJlzWTI/AAAAAAAABEA/RgUbcMOmrbk/w698-h567-no/lapslas9a8s.png)

Next, let's modify the `home.html` template. We'll start by adding a header to our app. Adding a header requires us to add the `ion-nav-bar` to the `index.html` page.
```
<ion-nav-bar class="bar-positive">
</ion-nav-bar>
```
The title of the ion-view passed would display the header in the `ion-nav-bar`. So, in `home.html` add the title attribute to the `ion-view`. Let's also add a few elements for the user to sign in. We'll start by adding the [ion-content](http://ionicframework.com/docs/api/directive/ionContent/) to the home.html. Inside `ion-content` we'll create the input boxes and button. Here is the home.html:
```
<ion-view title="iBucketList">
    <ion-content>
        <div class="list list-inset">
            <label class="item item-input">
                <input type="text" placeholder="Username">
            </label>
            <label class="item item-input">
                <input type="password" placeholder="password">
            </label>
        </div>
        <div>
            <button class="button button-block button-assertive">
                Sign In
            </button>
        </div>

    </ion-content>
</ion-view>
```

Save the changes and you should be able to view the sign in form on the home page.

![Sign In Form in Home Page](https://lh6.googleusercontent.com/-uVotiEOZ4cE/VSkkAY9sa7I/AAAAAAAABEc/aijXW5pe5OA/w700-h500-no/77ys7syd7sd.png)

It seems like the Sign In button is a bit too stretched. Let's add some padding to it's container. Inside css/style.css, add a style:
```
.padding{
	padding: 10px;
}
```
Apply the `padding` style to the button parent div.
```
<div class="padding">
    <button class="button button-block button-assertive">
        Sign In
    </button>
</div>
```
Save the changes and you should be able view the new sign in form.

![SignIn Page](https://lh5.googleusercontent.com/-QXKOmYEOHDA/VSklTXlHCvI/AAAAAAAABEs/Jk_BZqqBS0I/s567-no/alpala0a09aa.png)

## Implementing Sign In Functionality
We'll be using Firebase as back end for our Bucket list app. Register on [Firebase](https://www.firebase.com/) if you don't have an account already. Once registered you should have your own Firebase URL. Here is my firebase URL:
```
https://burning-fire-1723.firebaseio.com
```
In order to use [Firebase](https://www.firebase.com/), we need to include the following script references in `index.html`.
```
<script src="https://cdn.firebase.com/js/client/2.0.4/firebase.js"></script>

<script src="https://cdn.firebase.com/libs/angularfire/0.9.0/angularfire.min.js"></script>
```
Once references have been added, inject the `Firebase` module in the application. Modify the `controller.js` file to inject the Firebase module.
```
angular.module('starter.controllers', ['firebase'])
```
Inject `$firebaseAuth` in the HomeCtrl.
```
.controller('HomeCtrl',['$scope','$firebaseAuth', function($scope,$firebaseAuth)
```
Next in the `home.html` page, add the `ng-model` directive to the username and password input elements.
```
<label class="item item-input">
    <input type="text" placeholder="Username" ng-model="login.username">
</label>
<label class="item item-input">
    <input type="password" placeholder="password" ng-model="login.password">
</label>
```

Add the [ngClick](https://docs.angularjs.org/api/ng/directive/ngClick) directive to the sign in button.
```
<button ng-click="signin()"  class="button button-block button-assertive">
  				Sign In
</button>
```

In the HomeCtrl, define a function called `signin` which would be invoked when the user clicks the Sign In button.
```
$scope.login={};

$scope.signin = function() {
    var username = $scope.login.username;
    var password = $scope.login.password;

    console.log(username, password);
}
```
Save the changes and try to sign in after entering the username and password. If all goes well you should be able to see the username and password in the browser console.

Next, we'll try to authenticate against a user in Firebase. In order to make it work, first we'll create a `Firebase` object using the Firebase URL.
```
var firebaseObj = new Firebase("https://burning-fire-1723.firebaseio.com");
```
Using the firebaseObj we'll create a `loginObj`.
```
var loginObj = $firebaseAuth(firebaseObj);
```
Now when the user clicks the Sign In button, we'll use the [$authWithPassword](https://www.firebase.com/docs/web/libraries/angular/api.html#angularfire-users-and-authentication-authwithpasswordcredentials-options) API to authenticate against Firebase.
```
loginObj.$authWithPassword({
        email: username,
        password: password
    })
    .then(function(user) {
        //Success callback
        console.log('Authentication successful');

    }, function(error) {
        //Failure callback
        console.log('Authentication failure');
    });
```

Here is the modified HomeCtrl code:
```
.controller('HomeCtrl', ['$scope', '$firebaseAuth', function($scope, $firebaseAuth) {

    $scope.login = {};
    var firebaseObj = new Firebase("https://burning-fire-1723.firebaseio.com");
    var loginObj = $firebaseAuth(firebaseObj);

    $scope.signin = function() {
        var username = $scope.login.username;
        var password = $scope.login.password;

        loginObj.$authWithPassword({
                email: username,
                password: password
            })
            .then(function(user) {
                //Success callback
                console.log('Authentication successful');

            }, function(error) {
                //Failure callback
                console.log('Authentication failure');
            });

    }
}])
```

Save the above changes and try to sign in using username, `sam@sam.com` and password `sam`. On successful authentication you should have a success message in your browser console.

Let's create a user home page to redirect the user once successfully authenticated. In the templates folder add a page called `userHome.html`. Here is the `userHome.html`:
```
<ion-view title="iBucketList">
     <ion-content>
     <div class="userHomeMsg">
        <span>
        	<h2>Succesfully Logged in !!</h2>
        </span> 
      </div>
    </ion-content>
</ion-view>
```

Add a new state called userHome for the userHome.html page.
```
.state('userHome', {
    url:'/userHome',
    templateUrl:'templates/userHome.html',
    controller:'UserHomeCtrl'
  })

```
Create the controller `UserHomeCtrl` inside the `controller.js` file.
```
.controller('UserHomeCtrl', ['$scope', function($scope){
    
}])
```
Now on successful authentication, we'll redirect the user to the user home page. Inject `$state` in the HomeCtrl.
```
.controller('HomeCtrl',['$scope','$firebaseAuth','$state', function($scope,$firebaseAuth,$state)
```
On the success callback of the `$authWithPassword` API call, redirect to the `userHome` state.
```
loginObj.$authWithPassword({
        email: username,
        password: password
    })
    .then(function(user) {
        //Success callback
        console.log('Authentication successful');
        $state.go('userHome');

    }, function(error) {
        //Failure callback
        console.log('Authentication failure');
    });
```

Save the changes and try to sign in using username `sam@sam.com` and password `sam`. On successful authentication you will be redirected to the user home page.

![iBucket List App Screens](https://lh5.googleusercontent.com/U73vsY0AUZcihAhpE6wmFEw4_rwezKPdG1pwdcON_4Y=w900-h500-no)

## Wrapping It Up
In this tutorial, we learnt how to get started with creating a simple Bucket List app using IONIC framework and Firebase,  developing the sign in and sign up forms and user home page. 

In this next tutorial, we'll implement the sign up functionality for the bucket list app. Do let us know your thoughts, suggestions or any corrections in the comments below.
