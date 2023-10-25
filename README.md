Setting up Flask <br />
PetFax: Activities Directory <br />
[PetFax Part 1](https://github.com/michaelangelesz/PY_PetFax/blob/main/README.md#petfax-part-1) <br />
[PetFax Part 2](https://github.com/michaelangelesz/PY_PetFax/blob/main/README.md#petfax-part-2) <br />
[PetFax Part 3](https://github.com/michaelangelesz/PY_PetFax/blob/main/README.md#petfax-part-3) <br />


# PetFax Part 1

## Activity: PetFax Introduction: Flask Installation
We have been asked by a local animal shelter to create an application that shares fun animal facts alongside photos of the animals available for adoption. They hope this will be a fun way to get potential adoptees to engage with the shelter and find the animals loving new homes.

They just want us to create a proof of concept so let's use this opportunity and use a whole new stack to build the application. We will use Python and Flask, and no database for this initial sample.

They have given us some data to play around with, so let's get started!

__Setup__ <br />
Start by cloning this directory. It only holds the JSON data the shelter has given us.
```
git clone https://github.com/HackerUSA-CE/PY-petfax-app.git
```
[GitHub Repo](https://github.com/HackerUSA-CE/PY-petfax-app.git)

__Instructions:__

• Open your terminal. <br />
• Navigate to the location where you want the cloned directory. <br />
• Clone this repository with the git terminal command above. <br />
• Open the cloned repository in your code editor of choice. <br />
• Open the **pets.json** file and take a second to analyze the data structure. We won't use it for a little while, but it is still good to look it over before starting. <br />

## Installing Flask
Before we can get started, we have to install the Flask package. However, in order to do so we first need to create a virtual environment to help manage the dependencies for this particular project.

__In terminal:__

• Make sure you are in the root of the petfax-app project.<br />
• Using Python 3 built-in `venv` model, create a virtual environment and name the directory venv.<br />
•Once the virtual environment directory is created, activate it.<br />
  (Reminder: To later disconnect from the virtual environment, you can use the `deactivate` command.)<br />
  
__What your terminal commands should look like:__ <br />

__Mac:__
```
python3 -m venv <env_name>                
. <env_name>/bin/activate           
```
__Windows:__
```
python -m venv <env_name>
.\<env_name>\Scripts\activate
```

__In terminal:__

• Make sure your virtual enviroment was successfully started. You should see venv or something similar in terminal.<br />
• With our virtual environment set up, we can now install the Flask package with pip.<br />

__What your terminal commands should look like:__ <br />
```
pip install Flask           
```

## Create a Simple Flask Application
Before we get started with PetFax in earnest, let's get our bearings with this new framework first by creating a simple GET route. This way, we can be sure we have set everything up and have Flask working correctly before we dive into things.

By default, Flask assumes a basic entry point file will be named app.py. In most cases if there is no file named that way, it will not run. You can specify your entry file name when running the app if you desire a different name, but it is much easier to just use the default. For now, we will make a file named app.py so we can easily practice.

__In terminal:__

• Create a file named app.py<br />
• Open the file in your code editor.<br />
• In app.py, import the Flask package as `flask`.<br />
• Create an `app` instance from Flask. Be sure to pass it the special dunder variable __name__<br />

__What your code should look like:__ <br />
```
# config                    
from flask import Flask
app = Flask(__name__)
```

Great, we have now created a Flask app! Of course, it doesn't do very much right now. Let's give it something to do by writing a simple GET route.

__In app.py:__

• As we just learned, to create a route we need to call `.route()` on the app instance.<br />
• The method expects at least one argument specifying what endpoint to use for the route. Let's just have it go to '/'<br />
• To tell our route what to do when that endpoint is used, we need to define a method directly underneath it. Let's name our method `index`<br />
• Have the method simply return a string that says `'Hello, this is PetFax!'`<br />

__What your code should look like:__ <br />
```
# config                    
from flask import Flask
app = Flask(__name__)

# index route
@app.route('/')
def index(): 
    return 'Hello, this is PetFax!'
```

## Running a Flask Application
Great! We now have a small Flask app that just returns a string on the base index route. Now what? How exactly do we a run a Flask application? Thinking back, for Node.js apps, we could use npm run. Thankfully, Flask has a very similar command: flask run.

Wait! You may have noticed that we didn't specify a port anywhere for our app to listen on. Do we need to? Nope! By default, Flask will run on port 5000, so we don't have to. Let's try it out then!
```
flask run                           
```
If successful, you should see some messages in terminal telling you it is running on port 5000. You should also be able to go to port 5000 in your browser (at __http://127.0.0.1:5000/__ ) and see the string that we wrote.

__In terminal:__

![image](https://github.com/michaelangelesz/PetFax_Flask_Installation/assets/125311967/b8f538ac-6d91-40cf-a7cd-c4e6324b25fd)<br />
From: ThriveDX

__In the browser:__

![image](https://github.com/michaelangelesz/PetFax_Flask_Installation/assets/125311967/b37b9f80-7211-48e2-8e10-f848ee4cfdc9)<br />
From: ThriveDX

## Running a Flask Application with Reloading
For testing purposes, let's go ahead and make a second route.

__In app.py:__

• Underneath the index route we just wrote, create another one that goes to '/pets'<br />
• Define a method for this route called pets<br />
• Have the method simply return another string, this time saying 'These are our pets available for adoption!'<br />

__What your code should look like:__
```
# pets index route
@app.route('/pets')
def pets(): 
    return 'These are our pets available for adoption!'
```
Our app is already running, so in theory we should just be able to check out this new route we created in the browser immediately.

Try it out by going to __http://127.0.0.1:5000/pets__

Uh-oh! That is not what we want, and it doesn't make sense either. We definitely have a route that goes to `/pets`, so why isn't this working?

This happens because `flask run` does not automatically restart when a file changes. To apply any changes made after the initial run, you would have to manually stop and restart the server.

That can become tedious, of course, but thankfully there is a way around that. We simply have to use the `--reload` flag when running the command. That will make Flask automatically restart when a file has been changed. Try it out and then make a small change in either of your routes.
```
flask run --reload                
```

## Conclusion
As we have just experienced, starting a basic Flask application is incredibly simple, fast, and lightweight. That is one of the biggest benefits of using a micro framework.

Of course, such a small app isn't very useful, nor would it be very scalable to simply put all your routes on a single-entry file. In the next lesson, we will learn about some ways to better structure our application-and we will truly get started on PetFax!
<hr />

# PetFax Part 2

## Activity: Following the Application Factory Pattern
In the last activity, we started working on PetFax. We set up Flask to ensure we were able to get it working. In this activity, we will reorganize our app to be a little more robust and scale-friendly before we really dig into it.

__Getting Started__ <br />
• Open your terminal. <br />
• Navigate to where you cloned the __petfax-app__ repository. <br />
• Open it in your code editor of choice. <br />
• Activate the virtual environment by running `. venv/bin/activate` in the root of the repository. <br />
• Run the app with `flask run --reload.` <br />

**Create the Application Factory** <br />
The first step to reorganizing our project is to create the application factory. As we learned, we essentially want to make our application a package to be imported into the entry file. As such, we need to create a nested project folder that contains an `__init__.py` file. Let's start with that.

__In terminal__ <br />
Make sure you're in the root of __petfax-app__.
Make a new directory called __petfax__.
Inside that new directory, touch an `__init__.py` file.

__What your file structure should look like__ <br />
![image](https://github.com/michaelangelesz/PY_PetFax/assets/125311967/7d5b38a7-a2d4-49d9-a930-59e7dd5a399c) <br />
With the file structure set up, we can now work on the actual application factory. The `__init__.py` file is where we want to initially configure Flask and write the function that will create the instance of our app. Let's do that.

**`__init__.py`** <br />
• At the top of the file, import the `flask` package as `Flask`. <br />
•Define a function that will be our application factory. Let's call it `create_app`. <br />
• Inside that function, create a new `app` instance of `Flask`. <br />
• Still inside the function, create a basic index route that goes to '/' and just returns `'Hello, PetFax!'` as a string. <br />
• Lastly, don't forget to return the app instance at the end of the factory. <br />

__What your code should look like__ <br />
```
from flask import Flask 

def create_app(): 
    app = Flask(__name__)

    @app.route('/')
    def hello(): 
        return 'Hello, PetFax!'

    return app
```
Aside from creating the function and writing our app configuration within it, all of that should feel familiar. In fact, if you open up the __app.py__ file we previously wrote, you'll see it looks nearly identical.

However, that now leaves us with duplicate code. We no longer need the Flask configuration and routes inside the __app.py__ file since our **__init__.py** handles it instead. Let's get rid of it.

**__app.py__** <br />
• Delete everything in the file. <br />
• As the __init__.py configures everything, we can now import the petfax folder as a package. <br />
• Specifically, we want to import the application factory function that we wrote. Import create_app from the petfax folder. <br />
• Now that we have access to the factory function, we can create an app instance in app.py by invoking the function and saving it to a variable called app. <br />
• Test that everything's still working as intended by running `flask run --reload` <br />

**What your code should look like**
```
from petfax import create_app
app = create_app()
```
Note: Creating a global app instance with the application factory is different from creating it directly with Flask. Here, we're creating the app instance with all our custom logic already loaded into it.

__Conclusion__ <br />
We've now successfully reorganized our Flask application! However, it still doesn't do much. We learned about how to accept other HTTP methods for our routes, but we can't put it into play just yet. This is because we have no views. As this isn't an API, there's no way a user could POST without a new page, for example.

Additionally, our main reason for reorganizing to follow the application factory pattern is to take advantage of separating logic into different files. In other words, we want to be able to write something like the controllers in Express.

In the next lesson, we'll learn how to do both of those things!
<hr />

# PetFax Part 3
still working on*****

## Activity: Creating the Pet Blueprint and View
In the last activity, we reorganized our PetFax Flask app to allow for modularizing logic. In this activity, we'll break our routes into a separate blueprint and serve a proper index view.

**Getting Started** <br />
• Open your terminal. <br />
• Navigate to where you cloned the **petfax-app** repository. <br />
• Open it in your code editor of choice. <br />
• Activate the virtual environment by running `. venv/bin/activate` in the root of the repository. <br />
• Run the app with `flask run --reload`. <br />

## Creating the Blueprint <br />
Before we can even decide what our blueprint will be, let's remind ourselves what we're building. A local animal shelter has asked us to create an application that displays the pets up for adoption along with a fun fact about the species. If we look at the given data, we can see that the main focus is the pet.

As such, it would make sense for our blueprint to be a 'pet' blueprint. Let's get started on that.

**In terminal** <br />
Create a pet.py file on the same level as the __init__.py file. <br />
Open that file in your code editor. <br />
At the top of the file, import Blueprint from flask. <br />
Create a new instance of Blueprint and save it to a variable called bp. <br />

**Remember, creating a new blueprint instance requires three arguments:** <br />
The name of the blueprint. Let's name ours pet.
The location of the blueprint. We can just use the handy __name__.
The URL prefix that should be used for all routes attached to this blueprint. Let's go with /pets.
Our app is small, so it's fine to just have our blueprint on the same level as our __init__ file. When apps get larger, it can be a good idea to create separate folders for blueprints.

**What your code should look like:** <br />
undefinedClick here to copy
We can't quite test this blueprint yet. We need to add some routes before we can do that. So, let's add an index.

**pet.py** <br />
Define a route on the blueprint instance that goes to '/'. <br />
Define a method for the route named index. <br />
In the index method, return a string (for example: 'This is the pets index'). This is just for testing purposes. <br />

**What your code should look like:** <br />
undefinedClick here to copy
If we tried to test this out by going to http://127.0.0.1:5000/pets, it would not work yet. Why not? 

**We made some typos.** <br />
We should have created the route on the app instance, not on the blueprint. <br />
We need to import the app into the blueprint file. <br />
We have not registered the blueprint in the application factory. <br />

**Registering the Blueprint** <br />
To let the application know of the blueprint's existence, we need to register it in the factory.

**__init__.py** <br />
Above where we return the app in create_app, import the pet file. <br />
Underneath that, call the register_blueprint method on the app instance. <br />
Pass the pet blueprint into the method. <br />

**What your code should look like:** <br />
undefinedClick here to copy
Now we should be able to successfully test the /pets route in the browser. Try it out at http://127.0.0.1:5000/pets.

**Rendering Views**
We've finally completed the basic setup of our app. With that out of the way, we can start focusing on rendering templates.

**In terminal**
Jinja is built into Flask by default, so we do not need to do any installations or configuration to use its templating. All we have to do is create a templates folder that Jinja will use when looking for files to render. <br />
In that folder, create an index.html file. We don't need to use any custom Jinja file extensions, we can simply use HTML. <br />
In the index.html file, autocomplete the HTML boilerplate using your code editor's shortcut. <br />
In the body, create an h1 tag that says Welcome to PetFax. <br />

**What your code should look like:**
undefinedClick here to copy
If we go to /pets again, nothing will have changed. This template we just created won't be used yet because we have not actually told the route to render it.

**petfax/pet.py**
At the top of the file where we imported Blueprint from flask, add render_template to the import list. <br />
In the index method for the index route, instead of returning a string, return render_template and pass it the index.html template. <br />

**What your code should look like:**
undefinedClick here to copy
Now if we go to http://127.0.0.1:5000/pets, we should see our template being rendered!

**Displaying Data**
With our template successfully rendered, we can now focus on displaying the given data. The data was given to us in JSON file format, as opposed to a database. To use this data, we will have to utilize a few functions that Python has available:

open() to open files. This is a built-in function. <br />
json.load() to decode JSON. The base json package will have to be imported. <br />

**petfax/pet.py**
At the top of the file with our other imports, import json. <br />
Underneath that, we can open() the pets.json file by passing it as an argument. <br />
Once that file is opened, however, it still isn't readable for Python. This is where json comes in. Pass the entire open function as an argument to json.load(). <br />
Save that decoded JSON file to a variable. Let's name it pets. <br />
To ensure we loaded it in correctly, print the pets variable. Once you save the file, you should see the data in terminal. <br />

**What your code should look like:**
undefinedClick here to copy
Now that we have access to our data, we can pass it to the template as a variable. In our template, we can then loop through it using embedded Python.

**petfax/pet.py**
In the index route method, pass the render_template a second argument. Let's name it pets as well and pass it the pets variable that we just loaded with data. <br />
Now in templates/index.html, we can loop through the data using the pets variable. <br />
Loop through it using embedded Python and display:
pet_name as an h2
pet_photo as an img
Remember, for embedded Python, we use:
{{ }} for inserting variable values.
{% %} for evaluating Python logic.
end<statement> to end the evaluation. For example, endif to end an IF statement, or endfor to end a for loop. <br />

**What your code should look like:**
undefinedClick here to copy
undefinedClick here to copy
Check out the new pets index page! We should now see images of the actual pets.

Gif of the index view

**Conclusion**
With just blueprints and views, our app is looking much better. It would be nice to style the index though, wouldn't it? You'll learn how to add styling and static files in the next activity.

<br /><hr />

### Sources for photos used: 

- Dog: [Karseten Winegeart on Unsplash](https://unsplash.com/photos/5PVXkqt2s9k)
- Cat: [Alvan Nee on Unsplash](https://unsplash.com/photos/ZCHj_2lJP00)
- Rabbit: [Emiliano Vittoriosi on Unsplash](https://unsplash.com/photos/3FSBkX4yG80)
