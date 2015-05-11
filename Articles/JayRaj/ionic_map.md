In this tutorial, we'll see how to use Google Maps while developing mobile apps using [IONIC](http://ionicframework.com/). Using this app the user would be able to mark a particular position on the map, fill in some description and save the location in database. We'll be creating a custom directive to integrate Google Maps into our app. For saving the data we'll make use of [Firebase](http://firebase.com/).

Source code from this tutorial is available on [GitHub](https://github.com/jay3dec/iMapApp).

## IONIC Framework
IONIC is a mobile application framework for developing hybrid apps using HTML5. It uses AngularJS to create rich and robust mobile applications.
From the official site,

> Free and open source, Ionic offers a library of mobile-optimized HTML, CSS and JS components, gestures, and tools for building highly interactive apps. Built with Sass and optimized for AngularJS.

### Getting Started
Start by installing Node.js which would also install the node package manager npm.

Using npm install IONIC.
```
npm install -g cordova ionic
```
We'll be focusing on creating mobile app for Android platform, so make sure you have the required dependencies installed.
Once platform dependencies are installed create a blank IONIC project.
```
ionic start iMapApp blank
```
Navigate to the project directory `iMapApp`, add the required platform, build and emulate.

```
cd iMapApp
ionic platform add android
ionic build android
ionic emulate android
```
You should have the blank app running in the Android emulator.

Running the app each time on the emulator would be a time consuming task, so we'll make use IONIC cli to run the app in browser. Install the required dependencies using npm.
```
npm install
```
Once dependencies are installed, run `ionic serve` in the terminal and you should have the app running in the browser.

## Creating the User Interface
Let's start by adding a new template for the displaying our map. Inside the project directory create a folder called `www/templates`. Inside `templates` create a file called `map.html`.
```
<ion-view title="iMap">
    <ion-content>

        <div>
            <div id="map">
            </div>

            <div width="80%" class="list list-inset" style="margin-left:10%;margin-right:10%;">
                <label class="item item-input">
                    <input type="text" ng-model="user.desc" placeholder="Description">
                </label>

                <button class="button button-full button-positive" ng-click="saveDetails()">
                    Save
                </button>
            </div>
        </div>

    </ion-content>
</ion-view>
```
Inside map.html we have a div `#map` where we'll render our Google Map. Below the map we have added an input text box for the user to enter a description and a button to save the details.

We'll make use of [ionNavView](http://ionicframework.com/docs/api/directive/ionNavView/) directive to render different templates based on different states. Let's add the ionNavView directive to the `www/index.html` page. Above the ionNavView add the ionNavBar directive to create a top bar. Here is how the modified `index.html` looks like:
```
<body ng-app="starter">

    <ion-nav-bar class="bar-positive">
    </ion-nav-bar>

    <ion-nav-view></ion-nav-view>

</body>
```
 
Title for the ionNavBar is set from ionView which is rendered. And as seen in the above `map.html` code, we have set the title for the ionView.
IONIC uses Angular UI router module so as to organize app interfaces into different states. So, let's define a state for the `map.html` template. Open `www/js/app.js` and add the following code:
```
.config(function($stateProvider, $urlRouterProvider) {
    $stateProvider
        .state('map', {
            url: '/map',
            templateUrl: 'templates/map.html',
            controller: 'MapCtrl'
        })
 
    $urlRouterProvider.otherwise('/map');
});
```
In the above code we just defined a new state for URL `/map` which would render the template map.html and would be controlled by the `MapCtrl` controller which we'll define shortly.
We have used `$urlRouterProvider.otherwise('/map');` to set `/map` as the default state.

Inside `www/js/` create a file called `controller.js` and add a reference in the `www/index.html` file .
```
<script src="js/controller.js"></script>
```
We'll define all the controller code inside controller.js. Start by defining the angular module.
```
angular.module('starter.controllers', ['ionic'])
```
Define the controller `MapCtrl`.
```
.controller('MapCtrl', ['$scope', function($scope) {
// Code will be here
}]);
```
Inject the `starter.controllers` module in the `starter` app in `js/app.js`.

```
angular.module('starter', ['ionic','starter.controllers'])

``` 

Save the changes and you should be able to view the map.html template.

![enter image description here](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/04/1430422563imap_without_map.png)

 Next we'll add the Google Maps in `map.html`. For that we'll create a custom directive called `map`.
We'll be using this directive as an attribute, so let's start by defining the directive in `controller.js`.
```
.directive('map', function() {
    return {
        restrict: 'A',
        link:function(scope, element, attrs){
			// Code will be here
        }
    };
});
```
In map.html we have a div #map. Let's add the directive attribute to that div.
```
<div id="map" map> </div>
```
Google Maps would require some default parameters like zoom, latitude, longitude etc. We'll pass in those as parameters to the directive.
```
<div id="map" lat="-23.639492" lng="133.709107" zoom="8" map>

</div>
``` 
The above passed attributes can be accessed inside the directive's link  function using the parameter `attrs`.
```
.directive('map', function() {
    return {
        restrict: 'A',
        link:function(scope, element, attrs){

          var zValue = scope.$eval(attrs.zoom);
          var lat = scope.$eval(attrs.lat);
          var lng = scope.$eval(attrs.lng);
          
        }
    };
});
```

`scope.$eval` is used to evaluate the AngularJS [expressions](https://docs.angularjs.org/guide/expression).

Next include the Google Maps API reference in the `index.html` page.
```
<script src="https://maps.googleapis.com/maps/api/js?v=3.exp"></script>

```
Let's define Google Map's latitude and longitude using the default values.
```
var myLatlng = new google.maps.LatLng(lat,lng)
```
Define a few map options for our Google Maps,
```
mapOptions = {
  			    zoom: zValue,
  			    center: myLatlng
	  		  }
```
Now let's define the map with the above `mapOptions` and bind it to the `#map` div which can be accessed by `element[0]`.
```
map = new google.maps.Map(element[0],mapOptions)
```
Here is how the directive looks like:
```
.directive('map', function() {
    return {
        restrict: 'A',
        link:function(scope, element, attrs){

          var zValue = scope.$eval(attrs.zoom);
          var lat = scope.$eval(attrs.lat);
          var lng = scope.$eval(attrs.lng);
          
       
          var myLatlng = new google.maps.LatLng(lat,lng),
          mapOptions = {
  			  zoom: zValue,
  			  center: myLatlng
	  	  },
  	  	  map = new google.maps.Map(element[0],mapOptions);

    			
        }
    };
});
```
Add the following style to `www/css/style.css` to style up the `#map` div.
```
#map{
	width:80%;
    height:400px;
    margin:10px auto;
    box-shadow:0 3px 25px black;
}
```
Save the above changes and you should be able to view the Google Maps on the map page.

![enter image description here](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/04/1430424993map_without_marker_imap.png)

Let's also add a marker to the Google Maps.
```
marker = new google.maps.Marker({
  	position: myLatlng,
  	map: map,
  	draggable:true
})
```
We have set the default position of the marker as the latitude and longitude passed as attribute and set draggable option as true.
Here is the modified directive.
```
.directive('map', function() {
    return {
        restrict: 'A',
        link:function(scope, element, attrs){

          var zValue = scope.$eval(attrs.zoom);
          var lat = scope.$eval(attrs.lat);
          var lng = scope.$eval(attrs.lng);


          var myLatlng = new google.maps.LatLng(lat,lng),
          mapOptions = {
              zoom: zValue,
              center: myLatlng
          },
          map = new google.maps.Map(element[0],mapOptions),
          marker = new google.maps.Marker({
			    position: myLatlng,
			    map: map,
			    draggable:true
		  });


        }
    };
});
```
Save the above changes and you should have a draggable marker in the Google Maps.

![enter image description here](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/04/1430460025iMap_with_marker.png)

## Tracking Marker Position
We'll attach a drag end event to the Google Maps marker, so as to track the position of the marker.
So, inside the directive add the following code to attach a drag end event listener.
```
google.maps.event.addListener(marker, 'dragend', function(evt){
        console.log('Current Latitude:',evt.latLng.lat(),'Current Longitude:',evt.latLng.lng());    
});
```
Save the changes and try to drag the marker. Once you have stopped dragging the marker, check the browser console and you should have the current latitude and longitude.

## Saving the Details
Define a $scope variable called user in `MapCtrl`. It would contain the current position latitude, longitude and the description entered by the user.

```
$scope.user = {};
```
Create a function called `saveDetails` in the `MapCtrl` controller. This function would make use of the `$scope.user` variable to get the required data.
```
$scope.saveDetails = function(){
    var lat = $scope.user.latitude;
    var lgt = $scope.user.longitude;
    var des = $scope.user.desc;
    
    // Code to write to Firebase will be here
  }
``` 
When the user drags the marker on the map, we'll update the
`$scope.user.latitude` and `$scope.user.longitude` variables. So update both the variables in the drag end event listener's callback function.
```
google.maps.event.addListener(marker, 'dragend', function(evt){
    scope.$parent.user.latitude = evt.latLng.lat();
    scope.$parent.user.longitude = evt.latLng.lng();
    scope.$apply();
});
```
`scope.$apply` is called to update the model bindings.
Attach a [ngModel](https://docs.angularjs.org/api/ng/directive/ngModel) directive to the description input text box and [ngClick](https://docs.angularjs.org/api/ng/directive/ngClick) directive to the save button.
```
 <label class="item item-input">
        <input type="text" ng-model="user.desc" placeholder="Description">
 </label>
            
        <button class="button button-full button-positive" ng-click="saveDetails()">
```
Now let's save the data to firebase. Register for a free account on firebase if you haven't already. Once logged in you should have a unique firebase URL. My firebase URL is:
```
https://blistering-heat-2473.firebaseio.com
```
Sign in to Firebase account and click on the plus link next to the URL in the dashboard. Add name as `MapDetails` and value as `0` to create a sub URL, `/MapDetails`.

![enter image description here](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/12/1418823533jhakshd768.png) 

Include the following script references in the `index.html` to use firebase in our app.
```
 <script src="https://cdn.firebase.com/js/client/2.0.4/firebase.js"></script>
 
 <script src="https://cdn.firebase.com/libs/angularfire/0.9.0/angularfire.min.js"></script>
```
Inject firebase in the `starter.controllers` module in `controller.js`.
```
angular.module('starter.controllers', ['ionic','firebase'])
```
Inject `$firebase` module in the `MapCtrl` controller.
```
.controller('MapCtrl', ['$scope','$firebase', function($scope,$firebase)
```
Inside the `MapCtrl` create a firebase object using the firebase URL.
```
 var firebaseObj = new Firebase("https://blistering-heat-2473.firebaseio.com/MapDetails");
 
```
Using firebaseObj create an instance of `$firebase`.
```
 var fb = $firebase(firebaseObj);
```
Inside the `saveDetails` function, we'll make use of the firebase [push](https://www.firebase.com/docs/web/api/firebase/push.html) API to save data to firebase. 
```
fb.$push({
    latitude: lat,
    longitude: lgt,
    description: des
}).then(function(ref) {
    $scope.user = {};
}, function(error) {
    console.log("Error:", error);
});
```
Save the above changes and refresh the app. Drag the marker to a preferred position, enter a description and click save. Check firebase dashboard and you should have the data there.

 Once the data is saved we'll show an alert to notify the user. We'll make use of [ionic popup](http://ionicframework.com/docs/api/service/$ionicPopup/) to show pop up.
 Inject the `$ionicPopup` in the `MapCtrl` controller.
```
 .controller('MapCtrl', ['$scope','$firebase','$ionicPopup', function($scope,$firebase,$ionicPopup)
```
Add a function called `showAlert` in the `MapCtrl` controller.
```
$scope.showAlert = function() {
    $ionicPopup.alert({
        title: 'iMapApp',
        template: 'Your location has been saved!!'
    });
};
```
`showAlert` function would call the `$ionicPopup` service to show a pop with a title and template.
Call `showAlert` in the success callback of push API call.
```
fb.$push({
    latitude: lat,
    longitude: lgt,
    description: des
}).then(function(ref) {
    $scope.user = {};
    $scope.showAlert();
}, function(error) {
    console.log("Error:", error);
});
```

Save the changes and try to save the details again. Once the details have been saved in firebase you should have a pop up with a success message.

## Conclusion
In this tutorial, we saw how to use Google Maps in an IONIC mobile app. We saw how to create a custom directive to integrate Google Maps. You can extend the above shown functionality to create something useful. For an in depth info on using IONIC framework, I would recommend reading [official docs](http://ionicframework.com/docs/).

Do let us know your thoughts, suggestions and corrections in the comments below.


