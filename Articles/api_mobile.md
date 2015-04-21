# Building a simple REST API for mobile applications

## What is REST?
REST or Representational State Transfer is lightweight, HTTP based and runs on the same web servers web sites run on. Instead of delivering in HTML (a combination of presentation and data), it delivers data minimally with separators and delimiters (like JSON).  It's an architectural style for designing networked applications and a different way of delivering web services.  
REST is browsable so it helps developers modify and check the preciseness of their code, as only the data is displayed. It is a safer way of providing services or data access as it does not expose unnecessary surface area of the database used by the website.  Some more well-known REST apis are from [Twitter](https://dev.twitter.com/rest/public) and [Facebook Graph](https://developers.facebook.com/docs/graph-api).

REST is platform and language independent, although I recommend using PHP, Python or Ruby. There are four commonly defined methods used in REST architecture: the _create_, _read_, _update_ and _delete_ methods. We can add other more specialist methods like getting 'the top ten most popular items' or 'the highscore of all users' either by writing a new method or using a query parameter like `/api/items?top=10`.

## HTTP Methods and API endpoints

You might remember using the GET and POST requests when creating web forms (synchronous) or ajax requests (asynchronous). You’ve probably used PHP, Python or any other language to process form data. Through doing these things, you have  written your own simple REST framework.

POST, GET, PUT, DELETE correspond to create, read, update, delete (CRUD) and are  related to the most basic of database operations. API endpoints describe available operations on exposed data. Think of it as urls that provide data (GET request) or an url where you can submit data to (POST request).

There are many data formats we could use but the more common are JSON and XML.

## Using djangorest framework to build a simple REST api

I'm going to demonstrate how to build a simple REST api using the Django (Python MVC) and Django REST framework to  access data inside a database (just one table).  Django REST framework is built using Django (python) specifically for exposing data via the REST framework.  

Below are the steps and code to create the model and views. For ease of entering data, we will input them using the existing Django admin page.

To begin, you will need to have Python >v2.7 and Django v1.7.4 on your system.  If not, install [Python](http://www.python.org/download/) and [Django](https://www.djangoproject.com/download/) first.

You can test your installation by opening the command line, and typing the `python` command. You should see something like:

```
Python 2.7.6 (default, Nov 18 2013, 15:12:51)
[GCC 4.2.1 Compatible Apple LLVM 5.0 (clang-500.2.79)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

At the Python prompt, type:

```
>>> import django
>>> print(django.get_version())
```

This will output a version number and verifies that you have set up Django on your system. Exit out of the Python prompt and build the Django project.

```
django-admin.py startproject marine
```

This is the list of files and folders that should be created.

```
marine/
    manage.py
    marine/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```

Check if everything works by executing:

```
python manage.py runserver
```

This starts the Django development webserver for testing. If successful, you will see something like:

```
Performing system checks...

0 errors found
February 15, 2015 - 15:50:53
Django version 1.7.4, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

If you open the URL http://127.0.0.1:8000, you will see a placeholder website to show that everything is correct so far.

Now we will build an app (just a container) which houses a model (as in Model-View-Controller). A model is the source of data for your app. You can find more information about how to use models on the Django website or any other MVC related site.

```
python manage.py startapp fishes
```

Should result in the following files:

```
fishes/
    __init__.py
    admin.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

Currently inside the `models.py` file is only the import line `from django.db import models`.  Add the following code.

```python
    class Fish(models.Model):
        name = models.CharField(max_length=255)
        created = models.DateTimeField('auto_now_add=True')
        active = models.BooleanField()
```

This creates a class that exposes the name, created date of the fish and if the data row is active or not. Learn more about field types in [the Django documentation](https://docs.djangoproject.com/en/1.7/ref/models/fields/#field-types).

To register the fishes app, add it to the `marine/settings.py` file. Do this by adding `fishes` to the list under `INSTALLED_APPS`.

At this point, configure your database settings in `settings.py`, for this example you can use the default sqlite settings:

Run `python manage.py sql fishes` to get a preview of the database schema SQL that will run when we activate this app.  To confirm creating the relevant tables on the default sqlite database, type `python manage.py migrate` or `python manage.py syncdb` on older Django versions.

Now you have an empty `fish` table in your database and the model contains nothing. Luckily Django provides a built-in admin page that lets you quickly insert and modify data.  At the command prompt, type:

```bash
python manage.py createsuperuser
```

and follow the instructions to create an administrator's account.  You will use this account to log into the admin page.  Start the development server if you have not done so already with:

```bash
python manage.py runserver
```

Enter your username and password.  You should see a admin page with the _Marine_ list.  Click on _Fishes_ to add or modify data, add some data to it.

Up to this point, you have built a working, albeit plain, Django website.  We will now the incorporate Django REST framework to the site by downloading and installing it. [Find out how to do that here](http://www.django-rest-framework.org/#installation).  One key thing to remember is to add `rest_framework` into the `INSTALLED_APPS` list in `marine/settings.py` and add:

```python
url(r'^api-auth/', include('rest_framework.urls', namespace='rest_framework'))
```

To the `urls.py` file in the _marine_ folder.

When we installed the Django REST framework, it gave us the ability to use serializers, which flattens the data obtained from the fish model into a string format, either XML or JSON.  To create a serializer for the fish model, we create a file under the _fishes_ folder and call it `serializers.py`.  Add the following code to it:

```python
from fish.models import Fish
from rest_framework import serializers

class FishSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = Media
        fields = ('name', 'active', 'created')
```

And in the `views.py` file, add:

```python
from rest_framework import viewsets
from fishes.serializers import FishSerializer
class FishViewSet(viewsets.ModelViewSet)
    serializer_class = FishSerializer
```

If you now open _http://127.0.0.1:8000/api/fishes/_ you will see a browsable API.

```javascript
HTTP 200 OK
Content-Type: application/json
Vary: Accept
Allow: GET, POST, HEAD, OPTIONS

[
    {
        "name": "Dory",
        "created": "2014-06-21T04:23:01.639Z",
    },
    {
        "name": "Angel",
        "created": "2014-07-21T04:23:01.639Z",
    },
    {
        "name": "Clown",
        "created": "2014-08-21T04:23:01.639Z",
    }
]
```

## The iOS mobile app

Here I will detail the key steps required to create a mobile app that receives data from our API.  We are going to use the UI Table View to display our data in a list.  In XCode 6, create a new project:

File > New > Project > iOS Application > Single View Application

Product Name: Fishes
Language: Objective-C
Devices: iPhone
we do not use Core Data for now.

Select a location on disk to save your project and then click Create.

By default, the project will be created with a View Controller.  We will however, want to show the data from the REST api as a list, so we will use the Table View Controller instead.  So we will create a new set Objective-C files (File > New > File > iOS Source > Cocoa Touch Class).

Class: TableViewController
Subclass of: UITableViewController
we do not create a XIB file

You have just created the TableViewController.h and TableViewController.m files.

Go to the Main.storyboard, go to the Object library and drag the Table View Controller to the storyboard.  Select and delete the default View Controller.  Make sure that under Attributes Inspector, the checkbox for `Is Initial View Controller` for the selected Table View Controller is ticked.

In the Main.storyboard, expand the Table View Controller to expose Table View Cell then select the Attributes Inspector and enter FishCell in the Identifier.  Also change the Style to Subtitle from Basic.  This provides the utility to display the value set by `cell.detailTextLabel`.  This code below demonstrates the use of a simple NSArray to display data hardcoded in the UITableView.

```objectivec
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
#warning Incomplete method implementation.
    // Return the number of rows in the section.  We currently have two rows we would like to show
    return 2;
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"FishCell" forIndexPath:indexPath];
    //temporary data to demonstrate the structure of a NSDictionary in an NSArray, which is the general structure of a JSON
    NSArray *fishes = @[
                        @{@"name": @"Dory", @"created": @"2014-06-21T04:23:01.639Z"},
                        @{@"name": @"Angel", @"created": @"2014-07-21T04:23:01.639Z"},
                        @{@"name": @"Clown", @"created": @"2014-08-21T04:23:01.639Z"}
                        ];
    if (cell == nil) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"FishCell"];
    }
    //We will replace fishes with fishJson once we have code that downloads from the REST api
    [cell.textLabel setText:[[fishes objectAtIndex:indexPath.row] objectForKey:@"name"] ];
    [cell.detailTextLabel setText:[[fishes objectAtIndex:indexPath.row] objectForKey:@"created"]];
    return cell;
}
```
Next we need a way to obtain JSON from the REST api we published using django REST framework.  We first establish an NSArray object called `fishJson` by registering it in the @interface level and synthesizing it with `@property` and `@synthesize`.  This replaces the codes for the setters and getters.  We then replace the code we had in the `numberOfRowsInSection`, where we change `fishes` with `fishJson` which contain the JSON we downloaded from the REST api.
```objectivec
@interface TableViewController ()
@property (strong) NSArray *fishJson;
@end

@implementation TableViewController
@synthesize fishJson;
- (void) downloadData {
    //We use NSMutableString so we could append or replace parts of the URI with query parameters in the future
    NSMutableString *remoteUrl = [NSMutableString stringWithFormat:@"http://localhost:8000/api/fishes/?format=%@", @"json"];
    NSURLRequest *request = [NSURLRequest requestWithURL:[NSURL URLWithString:remoteUrl] ];
    NSError *jsonError = nil;
    NSHTTPURLResponse *jsonResponse = nil;

    NSData *response;
    do {
        response = [NSURLConnection sendSynchronousRequest:request returningResponse:&jsonResponse error:&jsonError];
    } while ([jsonError domain] == NSURLErrorDomain);

    if([jsonResponse statusCode] != 200) {
        NSLog(@"%ld", (long)[jsonResponse statusCode]);
    } else {
        NSLog(@"%@", @"200 OK");
    }
    NSError* error;
    if(response) {
        //fishJson was defined earlier near the top as a NSArray object
        fishJson = [NSJSONSerialization
                JSONObjectWithData:response
                options:kNilOptions
                error:&error];
    }
}
```
We now update the method number of rows in section.  The code makes sure that the number of rows matches the number of elements as contained in the fishJson array.
```objectivec
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
#warning Incomplete method implementation.
    // Return the number of rows in the section.
    return [fishJson count];
}
```
Now you have a working simple mobile app to display data obtained from an online or local REST api.  To run the mobile app on the iOS simulator, go to Product then Run.  If you have problems getting the iOS code error free, you can download it here.
