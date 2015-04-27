[React](http://facebook.github.io/react/) is a JavaScript library focused on building user interfaces. It has gained popularity among developers due to fact that it's created, used and maintained by Facebook.

## Why React ? 
React works on the concept of "virtual DOM" which makes it different. React maintains a virtual DOM and when a change occurs it updates the virtual DOM instead of updating the actual DOM. When there are a couple of changes in the virtual DOM, it makes a single update to the DOM. Thus avoiding frequent updates to DOM.

From the [official site](http://facebook.github.io/react/),

> React abstracts away the DOM from you, giving a simpler programming
> model and better performance. React can also render on the server
> using Node, and it can power native apps using React Native.

## Introducing Reapp.io 
[Reapp](https://reapp.io/) is a platform to create mobile apps. It provides a UI kit of components, optimized and fully customizable for creating mobile apps.

![Reapp Demo](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/04/1430115560reapp_demo_screen.png)  

## What we'll create
In this tutorial, we'll see how to create a mobile app using Reapp. We'll call this app, the "where was I" app. This app would help the user to save different locations where he had been. We'll make use of Google Maps API  to enable the user to select locations. We'll use [Firebase](https://www.firebase.com/) as back end to save the data.

Source code from this tutorial is available on [GitHub](https://github.com/jay3dec/ReactApp).

## Getting Started
We'll started by installing `reapp` and create a project called `ReactApp`.
```
npm install -g reapp
reapp new ReactApp
```
Navigate to the project directory, run reapp and you should have the 
app running at http://localhost:3010.
```
cd ReactApp && reapp run
```
Here is the project structure.

![ReactApp Project Structure](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/04/1430115552folde_str.png)

Inside the project directory we have the app folder which contains the `app.js` file. Different routes are defined in the `app.js` file. `components` folder contain different components that would be rendered when a particular route is requested.

## Creating View
 We'll start by removing the `sub.jsx` file from `components/home` folder. Open `home.jsx` and remove the existing code. 
 Let's start from scratch and try to understand how things work. We'll create a react class called `Home` to render our component. 
```
import { Reapp, React, View} from 'reapp-kit';

var Home = React.createClass({
  render: function() {
    return (
      <h1>Welcome to Reapp!!</h1>
    );
  }
});

export default Reapp(Home);
```

As seen in the above code, the render function returns the view to be displayed. 
Update the routes in the `app.js` file.
```
import './theme';
import { router, route } from 'reapp-kit';

router(require,
  route('home', '/')
);
``` 
Save the changes and restart the server. Point the browser to http://localhost:3010 and you should be able to view the default view. I would recommend [enabling device emulation](https://developer.chrome.com/devtools/docs/device-mode) from chrome developer tools to view the app as mobile app.

![enter image description here](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/04/1430115548welcome_reapp.png)

We'll try to integrate Google Maps into our view. Let's start by adding a header for our app. Modify the `home.jsx` to return a view inside the render function.
```
<View title="Where Am I">

</View>
```
Next we'll create a new map component to display Google maps. Let's start by adding the google maps API reference in the `assets/web/index.html` page.
```
<script src="https://maps.googleapis.com/maps/api/js?v=3.exp"></script>
```
In `home.jsx` let's create a new React component which would display the Google Maps.
```
var MapView = React.createClass({

    render: function() {
        return (
	        <div id="map"><span>Map Would be Here !!</span></div>
        );
    }
});
```
Add the MapView component in home view.
```
<View title="Where Am I">

	<MapView />
	<MapView />
</View>

```
Add the following style to the `assets/web/index.html` page.
```
<style>
    #map {
        width: 100%;
        height: 400px;
        margin: 0px;
        padding: 0px
    }
</style>
```

Save the changes and restart the server. You should have the text `Map Would be here !!` in your app screen.

## Adding Google Maps
We just saw how nesting react components work. So remove the span inside the `MapView` render function and replace it with actual map.
Once the component has been mounted we'll create the Google Maps and render it in the `#map` div. So, we'll write our Google Maps code in the `componentWillMount` lifecycle method.
In the `MapView` component add the  `componentWillMount` method.
```
componentDidMount: function() {
	// Code will be here
}
```
Inside `componentDidMount` define a default map location, map options and create the map.
```
var sitepoint = new google.maps.LatLng(-37.805723, 144.985360);

var mapOptions = {
        zoom: 3,
        center: sitepoint
    },
    map = new google.maps.Map(React.findDOMNode(this), mapOptions);
    
   this.setState({
       map: map
   });
```
In the above code we have used `React.findDomNode` to get a reference to the component's DOM node element. `setState` is used to trigger the UI updates.
Save the above changes and restart the server. If all goes well, you should be able to view the map.

![enter image description here](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/04/1430115543map_no_marker.png)

Let's also add a marker to our Google Maps. We'll also set a few options to our marker such as `animation` and `draggable`. 
```
marker = new google.maps.Marker({
     map:map,
     draggable:true,
     animation: google.maps.Animation.DROP,
     position: sitepoint
});
```
Here is the full `MapView` component:
```
var MapView = React.createClass({

    componentDidMount: function() {
      
      var sitepoint = new google.maps.LatLng(-37.805723, 144.985360);

      var mapOptions = {
              zoom: 3,
              center: sitepoint
          },
          map = new google.maps.Map(React.findDOMNode(this), mapOptions),
          marker = new google.maps.Marker({
           map:map,
           draggable:true,
           animation: google.maps.Animation.DROP,
           position: sitepoint
      });

      this.setState({
        map: map
      });
    },

    render: function() {
        return (
            <div id="map"><span>Map Would be Here !!</span></div>
        );
    }
});
```
Save the changes and restart the server and you should have the map with marker.

![enter image description here](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/04/1430115536map_marker.png)

## Adding Position Info

When the user drags the marker we'll show the position info. In order to implement that, let's add the required HTML in the Home component. Modify the render function code to look like this:
```
render: function() {
    return (
      <View title="Where Am I">
      
        <MapView />

        <div style={{width:100 + '%',height:100 + 'px',margin: 0 + ' auto',padding:10 + 'px'}} id="infoPanel">

            <div>
              <span><b>Position:</b></span>
              <span  id="info"></span>
            </div>

            &nbsp;

            <div>
              <span><b>Address:</b></span>
              <span  id="address"></span>
            </div>

        </div>
      </View>
    );
  }
``` 
Let's set the default position and address. For position, since we have hard coded the default latitude and longitude, set the info value as shown:
```
 document.getElementById('info').innerHTML = '-37.805723, 144.985360';
```
To display the address we'll make use [Google Maps Geocoder](https://developers.google.com/maps/documentation/geocoding/).
```
geocoder.geocode({
    latLng: marker.getPosition()
}, function(responses) {
    if (responses && responses.length > 0) {
        document.getElementById('address').innerHTML = responses[0].formatted_address;
    }
});
```
Here is the modified `MapView` component:
```
var MapView = React.createClass({

    componentDidMount: function() {
      
      var geocoder = new google.maps.Geocoder();
      var sitepoint = new google.maps.LatLng(-37.805723, 144.985360);

      document.getElementById('info').innerHTML = '-37.805723, 144.985360';
      
      

      var mapOptions = {
              zoom: 3,
              center: sitepoint
          },
          map = new google.maps.Map(React.findDOMNode(this), mapOptions),
          marker = new google.maps.Marker({
           map:map,
           draggable:true,
           animation: google.maps.Animation.DROP,
           position: sitepoint
      });

      geocoder.geocode({
        latLng: marker.getPosition()
      }, function(responses) {
        if (responses && responses.length > 0) {
            document.getElementById('address').innerHTML = responses[0].formatted_address;
        }
      });

      this.setState({
        map: map
      });
    },

    render: function() {
        return (
            <div id="map"><span>Map Would be Here !!</span></div>
        );
    }
});
```
Save the changes and restart the server and you should have the default position and address displayed in the app.

![enter image description here](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/04/1430115530map_with_info.png)

Let's add a `dragend` event listeners to update the position and address once the marker is dragged. Inside the `dragend` callback function, we'll get the marker position and address using which we can update the `address` and `info` element in the app.

```
google.maps.event.addListener(marker, 'dragend', function(e) {

    var obj = marker.getPosition();
    document.getElementById('info').innerHTML = e.latLng;

    map.panTo(marker.getPosition());

    geocoder.geocode({
        latLng: obj
    }, function(responses) {

        if (responses && responses.length > 0) {
            document.getElementById('address').innerHTML = responses[0].formatted_address;
        }
      
    });
});
```
Save the changes and restart the server. Now if you try dragging the marker, the info gets updated when dragging ends.

## Save Info in Firebase
Let's add a button to save the coordinates in [Firebase](https://www.firebase.com/). First we need to install `reapp-ui` into our project.
```
npm install reapp-ui@0.12.47
```
Import the button component in `Home.jsx`.
```
import Button from 'reapp-ui/components/Button';
```
Add the button to the Home component.
```
<Button onTap={this.savePosition}>Save </Button>
```
On `Save` button tap we'll define a function to save the coordinates to Firebase.
Register for a free account on Firebase to use it in our app. Once registered you should have the Firebase URL to start working. Here is my Firebase URL:
```
https://blistering-heat-2473.firebaseio.com
``` 
Login to your firebase account and click on the plus icon on the Firebase URL displayed in your dashboard to create a URL like:
```
https://blistering-heat-2473.firebaseio.com/Position
```
We'll use the above URL to save the location information.

Include Firebase reference in the `assets/web/index.html` page.
```
<script src="https://cdn.firebase.com/js/client/2.0.4/firebase.js"></script>
```
Next, let's define the `savePosition` function which will be called on the save button tap.
```
savePosition: function() {
    var wishRef = new Firebase('https://blistering-heat-2473.firebaseio.com/Position');
    var pos = document.getElementById('info').innerHTML;

    var address = document.getElementById('address').innerHTML;
    wishRef.push({
        'Position': pos,
        'Address': address
    });
}
```
As seen in the above code, we have create a Firebase object using the Firebase URL and have pushed the data to Firebase using [push API](https://www.firebase.com/docs/web/api/firebase/push.html).

Save the above changes and restart the server. Locate a position on the map and click save. Check firebase and you should have the data there.

Let's also add an alert to notify the user that the data has been saved. We'll make use of the modal component, so import modal in `Home.jsx`.
```
import Modal from 'reapp-ui/components/Modal';
```
Inside the Home View component's render function,  add the following modal code above `<MapView />`
```
{this.state.modal &&
          <Modal
            title="Coordinates Saved."
            onClose={() => this.setState({ modal: false })}>
          </Modal>
        }
```
This would only be visible when the `state.modal` is true. So, let's initialize `state.modal` to false when the app loads. For that we'll make use of the `getInitialState` method. Inside the `Home` component define the `getInitialState`.
```
getInitialState: function() {
    return {
      modal: false
    };
  }
```
Now inside the `savePosition` method after pushing the data to firebase, set the `state.modal` to true to show the modal.
```
this.setState({ modal: true });
```
Save the above changes and restart the server. Once the app has loaded, click on the `Save` button to save the data and you should be able to see the modal pop up.

![enter image description here](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/04/1430115524map_alert.png)

## Wrapping It  Up
 In this tutorial, we saw how to get started with creating a mobile app using ReactJS, Reapp and Firebase. We created an app to save the maps coordinates selected in the Google Maps to Firebase.
 
 I hope this tutorial serves as starting point for creating mobile apps using ReactJS. Do let us know your thoughts, suggestions or any corrections in the comments below.

