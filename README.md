# mern-notes

Ultimate MERN guide

In the terminal on you desktop

Cd ~
Cd projects
Mkdir name-of-project
Cd name-of-project
npx create-react-app client

In finder go to your projects folder and find name-of-project folder. Open name-of-project folder and add a folder Called server.

Back In the terminal on you desktop

Once you see Happy hacking! Enter the command code . This will open the project in VSCode.

In VSCode

Open a new terminal ( press control and  `)
Cd server
Npm init -y
(This will create a package.json file)
Open the package.json file and change: 
“main”: “index.js
To 
“main”:“server.js”

Back in the terminal in server:

npm i express cors dotenv nodemon axios mongoose body-parser

touch server.js
touch .env
touch .gitignore

Inside your .env file enter:
PORT=8080

Inside your .gitignore file enter:
node_modules
.env

Inside your server.js file you should have:

‘use strict’

const express = require(“express”)
const cors = require(“cors”)
const bp = require(”body-parser”) 
const axios = require(“axios”)

require(“dotenv”).config()

const app = express()
app.use(cors())
app.use(bp.json())
app.use(bp.urlencoded({extended: true}))
const PORT = process.env.PORT || 8080

app.listen(PORT, () => console.log(`server is running on port ${PORT}`))

This is the initial set up for the server complete.

Now lets do the initial setup for the client.

Delete the following files inside the src folder

App.test.js
Index.css
Logo.svg
Reportwebvitals.js
setupTests.js

Inside App.css 

Delete everything and add you css starter template.

Inside app.js Delete

import logo from './logo.svg';

 <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>

Inside index.js Delete

import './index.css';

import reportWebVitals from './reportWebVitals';

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();

Open another terminal in VSCode

cd into client.

Enter:

Npm i axios dotenv

Touch .env

Open .gitignore and under # misc enter:
.env

In the .gitignore file

Add .env under # misc

Example:
# misc
.env
.DS_Store
.env.local
.env.development.local
.env.test.local
.env.production.local

//******* side note

Inside our .env enter
REACT_APP_API_KEY=theKeyforAPI

then when we want to use our REACT_APP_API_KEY=theKeyforAPI

USE : ${process.env.REACT_APP_API_KEY}
For example:
const API = `http://www.omdbapi.com/?apikey=${process.env.REACT_APP_API_KEY}&t=${searchQuery}`;

if using un-secure API enter this code into your index.html head:

<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests" />


//*******

Inside the public folder locate and open index.html.

/*** - Not sure we should do this! Further investigation required.

Add to meta viewport:

, maximum-scale=1

***/

Change meta description to your description.

Change title to Title

Add your google font.

Change your favicon - google how to change this and make notes here.

Inside src folder create:

Components folder
Images folder
Pages folder

Inside components create

Header folder inside create
Header.js
Header.css

Footer folder inside create
Footer.js
Footer.css

Inside pages create
Home folder inside create
Home.js
Home.css
About folder inside create
About.css
About.js

Inside all the JS files just created type rcf enter and this will auto fill the following starter code example:

import React from 'react'

export default function Header() {
  return (
    <div>Header</div>
  )
}

Also inside all the JS files just created import the relevant css file.

Inside all the CSS files just created enter the css template:

import "./Header.css";

Create a reset.css file in src folder and add the css reset content from Eric Meyers.

Import the reset.css file into app.js.

Now include react-router-dom to navigate between pages.

Note :  React router is a library used for enabling client side routing.

In terminal make sure you are in the client and install:

npm i react-router-dom

In app.js

Import {BrowserRouter, Routes, Route}
from “react-router-dom”

Example code in App.js:

import “./reset.css”
import “./App.css”
import {BrowserRouter, Routes, Route} from “react-router-dom”
import Header from “./components/Header/Header”
import Footer from “./components/Footer/Footer”
import Home from “./Home”

function App(){
	return (
		<BrowserRouter>
			<div className=“App”>
				<Header />
				<Routes>
					<Route path=“/“ element={<Home />} />
				</Routes>
				<Footer />
			</div>
		</BrowserRouter>
	)
}


Once this is done read the React Helmet notes in the React Folder.

Using Link

In the following example we wrap an SVG with a link and link it to “/”

Example on Header component:

import React from “react”
import “./Header.css”
import logo from “../../images/airbnb-logo.svg”

import { Link } from “react-router-dom”

export default function Header(){
	return (
		<header className=“header”>
			<div className=“header-container”>
				<Link to=“/”>
					<img className=“logo” src={logo} alt=“company logo”>
				</Link>
			</div>
		</header>
	)
}

Now that we have the basic set up complete for the client.  Enter into the Header.js file: 

import React from "react";
import "./Header.css";

export default function Header() {
  return (
    <header className="header">
      <div className="header-container">
        <h1>This is the header</h1>
      </div>
    </header>
  );
}

Then enter the following into the Footer.js file:

import React from "react";
import "./Footer.css";

export default function Footer() {
  return (
    <footer className="footer">
      <div className="footer-container">
        <h6>This is the footer</h6>
      </div>
    </footer>
  );
}

The the following into the home page:

import React from "react";
import "./Home.css";

export default function Home() {
  return (
    <main className="main">
      <div className="main-container">
        <h3>this is the main homepage</h3>
      </div>
    </main>
  );
}

Next, in the client terminal enter:

npm start

This will display the frontend on localhost:3000.

Now in the server lets set our first endpoint:

"use strict";

const express = require("express");
const cors = require("cors");
const bp = require("body-parser");
const axios = require("axios");

require("dotenv").config();

const app = express();
app.use(cors());
app.use(bp.json());
app.use(bp.urlencoded({ extended: true }));
const PORT = process.env.PORT || 8080;

app.get("/", (request, response) => {
  response.json("This is the home route");
});


app.listen(PORT, () => console.log(`server is running on port ${PORT}`));

In the server terminal run: 
nodemon server

In the browser search localhost:8080

The page should load and display:
This is the home route.

Now lets set up mongoDB

Login to mongoDB

Where you folders are for you projects you can scroll down and set up a new project. 

Click new project.

Give your project a name click next
When testing I named the project memegen as it was on the meme-generator project.

We don’t need to add members and set permissions so click:

Create project

You will now be at the Database Deployments page. 

Click build a database.

Click create on the free shared option for learning and exploring MongoDB

Cloud provider - aws, google cloud azure???

Recommended region - generally go with recommended.

Go through settings change name to DemoCluster
When testing I named the project memegen as it was on the meme-generator project.

Create cluster

Create usename and password
When testing I set the username to Bipbipbip and the password to Cupoftea1

Click create user

Add entries to your IP access List

Set IP address to 0.0.0.0/0

Click finish and close.

A model will pop up and state
Congratulations on setting up access rules!
Click go to database

You will now be back at the Database Deployments page.

Click connect

Click connect using mongoDB compass.

Click the button to copy the connection string. Paste this so you have is stored somewhere.
On my test mine was:

mongodb+srv://Bipbipbip:<password>@memegen.ovpcsw4.mongodb.net/test

Click close.

On VSCode 

Create a new folder in server called models

Create a JS file inside models folder - example.js - this should be called something suitable. When setting up this example I used meme.js as it is in the meme-generator project.

In this file we will set up our Schema, the following example was Called Meme as the project was our meme-generator: 

const mongoose = require("mongoose")
const { Schema } = mongoose
const memeSchema = new Schema({
  name: String,
  color: String,
  heading: String,
  joke: Boolean,
})

const Meme = mongoose.model("Meme", memeSchema)
module.exports = Meme

Model is a method on mongoose that takes two properties the name of the model and then the schema of the model.

In server.js we require mongoose:
const mongoose = require(“mongoose”)

And we require the meme.js file we created for our schema from our models folder.
const Meme = require(“./model/meme”)

/*********
We also need to  put the following  in server.js

mongoose.connect(process.env.DATABASE_URL)

This is connecting this file to mongobd / our database / cluster

******

Our server.js file now has the following:

"use strict";

const express = require("express");
const mongoose = require("mongoose");
const Meme = require("./model/meme");

const cors = require("cors");
const bp = require("body-parser");
const axios = require("axios");

require("dotenv").config();

const app = express();
app.use(cors());
app.use(bp.json());
app.use(bp.urlencoded({ extended: true }));
const PORT = process.env.PORT || 8080;

mongoose.connect(process.env.DATABASE_URL)

app.get("/", (request, response) => {
  response.json("This is the home route");
});

app.listen(PORT, () => console.log(`server is running on port ${PORT}`));

Now in the .env file in your server enter:

DATABASE_URL=

Set this = to the connection string you copied from mongoDB

You should already have PORT=8080 so enter the DATABASE_URL after PORT.

Your .env file should now look like this:

PORT=8080
DATABASE_URL=mongodb+srv://Bipbipbip:<password>@memegen.ovpcsw4.mongodb.net/test

Before you save it make two changes to the connection string: 

Change password for the password you set and change test to something relevant. In this case we will say meme as the example is in our meme-generator.

Your .env file should now look like this:

PORT=8080
DATABASE_URL=mongodb+srv://Bipbipbip:Cupoftea1@memegen.ovpcsw4.mongodb.net/meme

Inside server folder create a file called seed.js

Inside type:

```
const mongoose = require("mongoose");
require("dotenv").config();
mongoose.connect(process.env.DATABASE_URL);
const Meme = require("./models/meme");

async function seed() {
  await Meme.create({
    name: "Superman meme",
    color: "red and blue",
    heading: "I'm faster than a speeding bullet",
    joke: true,
  });
  await Meme.create({
    name: "Free Guy",
    color: "blue",
    heading: "Don't have a good day, have a great day",
    joke: false,
  });
  console.log("Saved cool memes");
}

seed();
```

Look into mongoose.disconnect this would be added above seed()

Save the seed.js file

Go to mongoDB compass

Paste the DATABASE_URL in and click save and connect 

Give save connection to favourites a name - in this example we called it meme and choose green as the colour.

Open a new terminal 

Cd into server

Type node seed into the terminal

The terminal should return the string from the console.log in our seed.js file.

Go to mongoDB Compass refresh, meme will appear.

Click meme then click the memes folder and we will see our new data entries. The superman meme and the free guy meme.

We can now bin the terminal; where we set ran node seed.

//**********
note - if you get an error close the server terminal. 
open a new terminal cd into server and run nodemon server. This should now tell you what the error is.

Whilst setting this up I have had two errors in the schema. I wrote schema when deconstructing it with a lowercase s when is should have been an uppercase S for Schema.

I also got an error as when requiring (“./models/meme”) I wrote model instead of models.

Once these were corrected  node returned the response: 

Server is running on port 8080 which is what we wanted.
//**********

Now create some endpoints in server.js

//retrieve all memes
//retrieve specific meme
//add a new meme
//edit a meme
//delete a meme

// retrieve all memes
app.get("/memes", async (request, response) => {
  try {
    const allMemes = await Memes.find();
    response.status(200).json(allMemes);
  } catch (error) {
    console.log(error)
    response.status(500).json(error)
  }
});

Test this in thunder Client:
Make a get request to:
http://localhost:8080/memes
Click send
The feed back you get should be:
Status 200 OK
[
  {
    "_id": "63726bca4a4fa0977aa2276f",
    "name": "Superman meme",
    "color": "red and blue",
    "heading": "I'm faster than a speading bullet",
    "joke": true,
    "__v": 0
  },
  {
    "_id": "63726bca4a4fa0977aa22772",
    "name": "Free Guy",
    "color": "blue",
    "heading": "Don't have a good day, have a great day",
    "joke": false,
    "__v": 0
  }
]

Also check you get the same feedback in the browser:
http://www.localhost:8080/memes
This should give you the same response as above.

//retrieve specific meme
app.get("/memes/:id", async (request, response) => {
  try {
    const theMeme = await Memes.findOne({ _id: request.params.id });
    response.status(200).json(theMeme);
  } catch (error) {
    console.log(error)
    response.status(500).json(error)
  }
});

Test this in thunder Client:
Make a get request to:
http://localhost:8080/memes/63726bca4a4fa0977aa2276f
Click send
The feed back you get should be:
Status 200 OK
[
  {
    "_id": "63726bca4a4fa0977aa2276f",
    "name": "Superman meme",
    "color": "red and blue",
    "heading": "I'm faster than a speading bullet",
    "joke": true,
    "__v": 0
  }
]

Also check you get the same feedback in the browser:
http://www.localhost:8080/memes/63726bca4a4fa0977aa2276f
This should give you the same response as above.

//Add a new meme
app.post("/memes", async (request, response) => {
  try {
    const newMeme = await Memes.create(request.body);
    response.status(200).json(newMeme);
  } catch (error) {
    console.log(error)
    response.status(500).json(error)
  }
});


Test this in thunder Client:
Make a post request to:
http://localhost:8080/memes
Select body then copy and paste a previous meme object into the json section. Delete the “_id” and “__v”
Then change the other values of the properties. See this example below:
Post http://localhost:8080/memes
Body
Json
{
  "name": "Thomas Turner meme",
  "color": "dark blue",
  "heading": "I'm super T terra",
  "joke": false
}

Click send this should return:
Status 200 OK
{
  "name": "Thomas Turner meme",
  "color": "dark blue",
  "heading": "I'm super T terra",
  "joke": false,
  "_id": "6373b01dbd136ef23b4fa7a5",
  "__v": 0
}

Now do a get request to http://localhost:8080/memes to see all the memes your new meme should be included.

Also check in the browser http://localhost:8080/memes
To see all the memes.

//Edit a meme
app.put("/memes/:id", async (request, response) => {
  try {
    const memeToUpdate = request.params.id;
    const updatedMeme = await Memes.updateOne({ _id: memeToUpdate }, request.body);
    response.status(200).json(updatedMeme);
  } catch (error) {
    console.log(error)
    response.status(500).json(error)
  }
});

Test this in thunder client:
Make a put request to:
http://localhost:8080/memes/63726bca4a4fa0977aa22772
Select body then  paste the object into the json section. Delete any key value pairs that do not need to be edited. Then change the value to of the remaining properties that you wish to edit and update. Click send.
See the example below:
Put http://localhost:8080/memes/63726bca4a4fa0977aa22772
Body
Json
{
  "name": "Free Guy meme"
}
Status 200 OK
{
  "acknowledged": true,
  "modifiedCount": 1,
  "upsertedId": null,
  "upsertedCount": 0,
  "matchedCount": 1
}
This object response below status 200 OK is generated once you click send.

Now do a get request to http://localhost:8080/memes to see all the memes your meme that you edited should be updated.

Also check in the browser http://localhost:8080/memes
To see all the memes.


//Delete a Meme
app.delete("/memes/:id", async (request, response) => {
  const memeToDelete = request.params.id;
  const deletedMeme = await Memes.deleteOne({ _id: memeToDelete });
  response.status(200).json(deletedMeme);
});

Test this in thunder client:
Make a delete request to:
http://localhost:8080/memes/6373b01dbd136ef23b4fa7a5
Click send
This will return:
Status 200 OK
{
  "acknowledged": true,
  "deletedCount": 1
}

Now do a get request to http://localhost:8080/memes to see all the memes. Your meme that you deleted should not show as it will have been removed.

Also check in the browser http://localhost:8080/memes
To see all the memes.

Working on the front end

Add some basic styles to the header, homepage and the footer just to set up a layout.

We want our homepage to load all the memes in our database. To do this we write the following in Home.js:

First set up useStateSnippet: type uss and enter, the use state snippet format will appear. Rename the states. You should have the following:

const [memes, setMemes] = useState([])

For this example to get all memes we have set the memes state to an empty array.

At the top of the page type useState and press enter to give us the ability to use the useState method. This will appear as follows:

import React, { useState } from "react";

We can then delete the useState we just typed as it has been applied in the import React code.

Now set up your function:

const getMemes = async () => {
    const API = `http://localhost:8080/memes`;
    const res = await axios.get(API);
    console.log(res.data);
    setMemes(res.data)
  };

Then type useEffect and press enter. This will give us the ability to use the useEffect method. It will appear in the file as follows:

import React, { useEffect, useState } from "react";

 Now use useEffect to call getMemes when the page loads:

useEffect(() => {
    getMemes();
  }, []);

Reload the page and check the console to see if you have retrieved the data. 

Recap:
We have:
import React, { useEffect, useState } from "react";

import axios from "axios";

const [memes, setMemes] = useState([]);

 useEffect(() => {
    getMemes();
  }, []);

  const getMemes = async () => {
    const API = `http://localhost:8080/memes`;
    const res = await axios.get(API);
    console.log(res.data);
    setMemes(res.data);
  };

End of Recap

Create a new component called Memes - this is so we can map through and render the memes from our state.

Folder Memes 
Memes.js
Memes.css

Import Memes.css into Memes.js

Now import Memes into Home.js and place Memes into the main container. Also parse memes as a prop in Memes.

Example:

import React, { useEffect, useState } from "react";
import "./Home.css";

import axios from "axios";
import Memes from "../../components/Memes/Memes";

export default function Home() {
  const [memes, setMemes] = useState([]);

  useEffect(() => {
    getMemes();
  }, []);

  const getMemes = async () => {
    const API = `http://localhost:8080/memes`;
    const res = await axios.get(API);
    console.log(res.data);
    setMemes(res.data);
  };

  return (
    <main className="main">
      <div className="main-container">
        <Memes memes={memes}/>
      </div>
    </main>
  );
}
 
Example end

Now let’s get the memes to render on the page.

In Memes.js

First we need to parse memes as a prop.

Then we can return a fragment, and inside the fragment we map through memes, deconstruct the meme object (each object in the memes array) then create a div and render each property value as required.

Example:

import React from "react";
import "./Memes.css";
import { Link } from "react-router-dom";

export default function Memes({ memes }) {
  return (
    <>
      {memes.map((meme, idx) => {
        const { name, color, heading, joke } = meme;
        return (
          <div className="meme-container" key={idx}>
            <Link to="/">
              <h2>{name}</h2>
            </Link>
            <p>This meme is {color}</p>
            <p>{heading}</p>
            {joke && <p>This meme is a joke.</p>}
            {!joke && <p>This meme is not a joke.</p>}
          </div>
        );
      })}
    </>
  );
}

Example end
 
Alternatively we can not create the component and just create the map in Home.js.

Once created we can style to our liking.

Create a form to add a new meme

Two options you can either create the form on the page or create a component for the form.

Create a component called CreateMeme:
Folder: CreateMeme
JS: CreateMeme.js
CSS: CreateMeme.css

Include the component in the return on the home page.

Either in App.js or Home.js we need to create:

A use state snippet for the form called createForm.
A function called handleChangeCreate
A function called createNewBook

If we create these in app.js we will parse as props to Home.js then to CreateMeme.js. In this example we will create these in Home.js.

createForm use state snippet

const [createForm, setCreateForm] = useState({
    name: "",
    color: "",
    heading: "",
    joke: false,
  });

This state snippet set the state of create form to be an object with the same key value pairs as all of our memes. The initial values are empty. As joke is a boolean we have set it to false.

Create handleChangeCreate function

 const handleChangeCreate = (event)=>{
    setCreateForm({...createForm, [event.target.name]: event.target.value})
  }

Create createNewMeme function

const createNewMeme = async (event)=>{
  event.preventDefault()
  const API = `http://localhost:8080/memes`
  const res = await axios.post(API, createForm)
  //reset the input fields
  setCreateForm({
    name: "",
    color: "",
    heading: "",
    joke: false,
  });
  //add our new meme to the page
  setMemes([...memes, res.data])
}

This function is making a post request using axios to the url we set as API, the body/ content we are posting is createForm. The values of the properties in createForm have been set by the handleChangeCreate function before the post request is made. We then reset the values of the properties in createForm back to their original state. We then set the state of memes to be an array that includes all the indexes that were already in memes (these were objects - initially it was an empty array but on page load we ran useEffect to set memes to be an array with the objects from our database) and also include the value of res.data in the array. Res.data is the object we created with createForm.

Parse these as props

Now that these have been created we need to parse them as props to createMeme.

return (
    <main className="main">
      <div className="main-container">
        <Memes memes={memes} />
        <CreateMeme createForm={createForm} handleChangeCreate={handleChangeCreate} createNewMeme={createNewMeme} />
      </div>
    </main>
  );

Then in parse them in CreateMeme:

export default function CreateMeme({ createForm, handleChangeCreate, createNewMeme }) {
  return <div>CreateMeme</div>;
}

Set up the form

First we need to create a fragment to wrap a heading (create a new meme).

Then we can create our form.

We create the form using the form tag and we set the value of onSubmit to be createNewMeme so when the form is submitted it will run this function. Remember createNewMeme function will set memes to be everything it was as well as the new data/object that is parsed to it from createForm.

Inside the form we create the inputs. The inputs must have:
A name which is equal to the name of the property.
An onChange equal to the handleChangeCreate Function
A value equal to createForm.name

Example:
<input name="name" onChange={handleChangeCreate} placeholder="Meme name" value={createForm.name} required />

The name is equal to name, the value is equal to createForm.name. The handleChangeCreate function runs every time the input changes. When we type into the input field the value changes to whatever we type and the handleChangeCreate function changes createForm to be what it was but will change the property that is named the same as the value of name in the input and set the value of the property we are changing to be the same as the event target value which is whatever we type. Every time we type it updates the relevant key value pair in createForm.

Example:
<input name="color" onChange={handleChangeCreate} placeholder="Set meme color" value={createForm.color} />

The name of this input is color. Our createForm has a value called colour set to an empty string:

{
    name: "",
    color: "",
    heading: "",
    joke: false,
  }

The handleChangeCreate function will take create form as it is then update the color property as our event.target is the input and the event.target.name is color and it will set it to the new event.target.value. The value is initially createForm.color which is an empty string but as we type into the input field the value changes to what is typed.

Set the other inputs to be similar. The final form should look as follows:

handleCheck function

In our createForm we have a boolean, our joke property is set to false. We need to handle this differently. We need to create a handleCheck function. For this example we will create handleCheck in Home.js and parse it as a prop to createMeme.js.

Example:

 const handleCheck = (event) => {
    setCreateForm({ ...createForm, [event.target.name]: !createForm[event.target.name] });
  };

This function is changing the createForm to set it to everything that createForm currently is using …createForm. It then will update the property to that has the same name as the name of the input the function is attached to.  It will update the value to be the opposite of what createForm[event.target.name] currently is as we use the ! To state !createForm[event.target.name].

Example:

joke is a property of createForm which is set to false:

{
    name: "",
    color: "",
    heading: "",
    joke: false,
  }

Our input is a checkbox and it has a name attribute equal to “joke”. The value attribute is createForm.joke and the checked attribute is also createForm.joke.
So the value is false to start checked is a boolean and therefore is also set to false.   

<input
          name="joke"
          value={createForm.joke}
          checked={createForm.joke}
          onChange={handleCheck}
          type="checkbox"
          id="Joke"
        />

The onChange attribute calls the handleCheck function every time the value changes so when the checked box is checked the handleCheck function sets createFrom to everything it was and set the value of the property which has the same name as the event target name which In this case is Joke to be the opposite of what it currently is. So every time the checkbox is clicked it will change the value of Joke to be true if it is currently false and false if it is currently true.

Finally we need to add a button inside our form. We will create one for this example  that says create meme.

Now were ready to add css styles to our form.

The form should now be working and rendering the new memes that have been created onto the page.

Create a page for each object/meme

We now want to create a new page for each meme. This is so we can create a new form which will allow us to edit the details.

First we need to set up a page component. We will call this MemeDetails:

Folder: MemeDetails
JS: MemeDetails.js
CSS: MemeDetails.css

Fill JS file with template rcf and enter. Fill CSS file with css template.

Then we need to set up the Route to MemeDetails  in our App.js:

Example:

function App() {
  return (
    <BrowserRouter>
      <div className="App">
        <Header />
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/memes/:id" element={<MemeDetails />} />
        </Routes>
        <Footer />
      </div>
    </BrowserRouter>
  );
}

export default App;

Next in Memes.js we need to create a Link that will take us to the page for that meme. Inside Memes.js we map through the memes and name each object/meme as meme. We then deconstruct each object/meme to get the properties. Each object/meme has a property _id which a unique value.

For this example we create a link around the h2 element which renders the meme name. The path is set to {`/memes/${_id}`} this is the same path we set in the Route in App.js to take us to MemeDetails. We encapsulate the path in {} and `` template string so we can access with a template literal the _id of meme.

Example:

export default function Memes({ memes }) {
  return (
    <>
      {memes.map((meme, idx) => {
        const { _id, name, color, heading, joke } = meme;
        return (
          <div className="meme-container" key={idx}>
            <Link to={`/memes/${_id}`}>
              <h2>{name}</h2>
            </Link>
            <p>This meme is {color}</p>
            <p>{heading}</p>
            {joke && <p>This meme is a joke.</p>}
            {!joke && <p>This meme is not a joke.</p>}
          </div>
        );
      })}
    </>
  );
}

Set up MemeDetails.js   

First we need to create a useStateSnippet we will call ours meme as it holds the information of a meme. We will set the meme state to an empty object:

const [meme, setMeme] = useState({})

Remember we will also need to import useState.

We will then need to create a function called getMemeDetails which we retrieve the data of the specific meme that we want. 

To do this will need to make a get request using axios. To use axios we must import it from axios. The request will be to a path that ends with the id of the object/meme. We will need to grab the id from the url parameter we have for the page. To do this we had to use useParams() method. We must import useParams from react-router-dom to use it.

Example:

import React, { useState } from "react";
import { useParams } from "react-router-dom";
import axios from "axios"

export default function MemeDetails() {
  const [meme, setMeme] = useState({});

  const { id } = useParams();

  const getMemeDetails = async () => {
    const API = `http://localhost:8080/memes/${id}`;
    console.log(API)
    const res = await axios.get(API)
    setMeme(res.data[0])
  };

  return (
    <div>
      <h6>hey mememe</h6>
    </div>
  );
}

If there is an error that the meme with this id cannot be found we will set up an if statement that will render  and provide a link back to the homepage.

Note we will need to import Link to do this:

import { Link } from "react-router-dom";

Example:

if (!meme) {
    <>
      <h1>Woops. Thats a 404</h1>
      <p>The book with {id} no longer exist</p>
      <Link to="/">Go back to the homepage</Link>
    </>;
  }

Now that we have a function, that will retrieve the data of the meme with the id that has been placed as the parameter in the url and set the state of meme to that data , we need to invoke it on the page load using useEffect.

First we need to import the useEffect:

Import React,  {useState, useEffect } from “react

Then we can write our useEffect to invoke getMemeDetails on load:

Example:

 useEffect(() => {
    getMemeDetails();
  }, []);

Now on page load the state of meme will change from and empty object to an object filled with the meme key value pairs.

This will now allow us to setup the content on the page.

Example:

return (
    <div>
      <Link to="/">&#8617; Home</Link>
      <h1>{meme.name}</h1>
      <p>{meme.color}</p>
      <p>{meme.heading}</p>
      {meme.joke && <p>This meme is a joke</p>}
      {!meme.joke && <p>This meme is not a joke</p>}
    </div>
  );

At this stage you may wish to add some styles to make the page a little more readable.

Set up a form to edit the meme

First we need to create a use state snippet. That will hold the initial state of our form.

Remember we will also need to import useStart. This should have already been done in this project.

Example: 

const [formUpdate, setformUpdate] = useState({
    name: "",
    color: "",
    heading: "",
    joke: false
  })

Then we will set up our form that will render out on the page:

  return (
    <main className="meme-details-main">
      <div className="meme-details-main-container">
        <div>
          <Link className="meme-details-return-home-btn" to="/">
            &#8617; Home
          </Link>
          <h1 className="meme-details-heading">Meme Details</h1>
          <h2>{meme.name}</h2>
          <p>{meme.color}</p>
          <p>{meme.heading}</p>
          {meme.joke && <p>This meme is a joke</p>}
          {!meme.joke && <p>This meme is not a joke</p>}
        </div>
      </div>
      <section className="update-meme-form-section">
        <form onSubmit="">
          <input name="name" placeholder="Update meme name" value={formUpdate.name} />
          <input name="color" placeholder="Update meme color" value={formUpdate.color} />
          <input name="heading" placeholder="Update meme heading" value={formUpdate.heading} />
          <input name="joke" value={formUpdate.joke} checked={formUpdate.joke} type="checkbox" id="joke" />
        </form>
      </section>
    </main>
  );

Now maybe a good time to add some styles.

Our form is set up but it needs the onChange attribute added to all the inputs. Before we add these we need to create a function to handle the change. We will call it handleChangeUpdate.

Example:

const handleChangeUpdate = (event) => {
    setformUpdate({...formUpdate, [event.target.name]: event.target.value})
  }

The handleChangeUpdate function sets formUpdate to everything that formUpdate is and set the property with the same name as the event target  to the new value of the event target. [event.target.name]: event.target.value.

We also need to create an handleCheckUpdate function to update the checkbox input. We will call this handleCheckUpdate:

Example:

const handleCheckUpdate = (event) => {
    setformUpdate({ ...formUpdate, [event.target.name]: !formUpdate[event.target.name] });
  };

The handleCheckUpdate is setting formUpdate to everything it currently is then updating the property with the same name as the event target to be the opposite value to what that property currently is by using the ! . 

Create the updateMeme function

Here is the function:

  const updateMeme = async (event) => {
    event.preventDefault();
    const bodyToSend = {};

    for (const prop in formUpdate) {
      if (formUpdate[prop] !== "") {
        bodyToSend[prop] = formUpdate[prop];
      }
    }

    const API = `http://localhost:8080/memes/${id}`;
    const res = await axios.put(API, bodyToSend);
    console.log(res);
    getMemeDetails();
    setformUpdate({
      name: "",
      color: "",
      heading: "",
      joke: false,
    });
  };

First we create a variable bodyToSend and set it equal to an empty object.

Then we create a for of loop. That will go through every property of the formUpdate and execute an if statement if the property of the formUpdate, formUpdate[prop], does not equal and empty string, !== “”.  Then the value of the property will be what the value you already is in the meme object. For example if we are editing/updating a meme with the name superman meme and we leave this input empty for editing the name, the name property will still have the value of superman meme. This is bodyToSend[prop] = formUpdate[prop].

We then create our API variable which is a url path to the page with the id of our meme object. 

Then we make an axios put request to update the object. The put request is made to the API path which is our meme object by the id. The data we are sending to update is the bodyToSend object.

The function then invokes the getMemeDetails() function. Which makes a get request to retrieve the data of our object with the relevant id and sets meme to be an object with the new key value pairs.

Finally we set formUpdate to be all the properties with a value of an empty string and false for the boolean. Which resets all the input fields.


Delete a Meme

To delete a meme we will set up a function called deleteMeme. We will create this in Home.js as this is where we will be able to delete the meme from.

We will then parse it as a prop to Memes.

In Memes, where we map through memes to create and render each individual meme, we will create a button and set the onClick value to a callback function which triggers the deleteMeme function parsing in meme (meme is each individual meme object) as an argument.

The delete function:

 const deleteMeme = async (meme) => {
    const check = window.confirm(`are you sure you want to delete ${meme.name}`);
    //stop the rest of the function if they say no
    if (!check) {
      return;
    }

    const API = `http://localhost:8080/memes/${meme._id}`;
    const res = await axios.delete(API);
    if (res.data.deletedCount === 1) {
      getMemes();
    } else {
      alert("There was a problem deleting this book");
    }
  };

First we set meme as a parameter in the function. This is the same name we gave the argument when we invoked the deleteMeme() function in the onClick attribute of the delete button in our meme.

Then inside the function we create a variable called check and set the value equal to window.confirm method which asks you to confirm you want to delete the meme.

Window.confirm() instructs the browser to display a dialog with an optional message, and to wait until the user either confirms or cancels the dialog.

We then execute an if statement if check equals a false value then return.  The return takes us out of the whole function and stops it.

Next we set a variable called API equal to the url path of the meme via the id. We then make a delete request using axios to the API url path we set.

Following the delete request we execute an if statement that states if in the response date we get back deleteCount === 1 then we invoke getMemes() function which will set memes to all the meme objects in the database - note this should now not include the meme we just deleted as it has been removed from the database.

We also state if deleteCount is anything other than 1 then excite an alert to notify the user that there was an issue deleting the meme.

We have created a website where we can view the objects of a database, we can add a new object to that database, we can view each object on its own page where we can edit the details of that object and finally we can delete each of the objects from the database.

Link the project with git hub

Go to get hub make a new repo.

On your profile go to repository and click new

Click create repository

When we make a mono repo (client and server) we need to remove the hidden .git file from our client folder that create react app made.

In terminal in VSCode cd into client and run:

rm -rf .git

cd ..

git init

Copy the top line of the second box in GitHub

Example: 

git remote add origin https://github.com/CSEAMAN3/vans.git

git add .

Git commit -m “initial commit”

Git push -u origin main

Go to Netlify

Log in

Add new site

Import an existing project from GitHub

Find your repo

Site settings

Base directory = client

Build command = npm run build

Publish directory = client/build

Show advanced 

New variable

Key = CI
Value = false

Functions directory leave blank

Deploy site

Site settings 

Change site name to what you want it to be.

Now this has been done we can click the url and the front end will load.

Go back to cseaman3’s team

Add new site 

Import existing project

Find the project

Click into It.

Base directory = server

Build command = npm run build

Publish directory = server/dist

New variable

Key = CI
Value = false

New variable

Key = DATABASE_URL 
Value = mongodb+srv://Bipbipbip:Cupoftea1@vanscluster.75ejoa3.mongodb.net/vans

Functions directory functions

Before you deploy site do the following:

Inside server

Make a dist folder

Inside dist a file called index.html and leave it blank

Make a functions folder inside server

Make a src folder inside server

Move models folder and server.js into src folder

Rename  server.js to api.js

Make a new file in server called netlify.toml

Inside netlify.toml write 
```
[build]
functions = “functions”
```
Add

 “/.netlify/functions/api”

To the start of every endpoint in api.js

Add the following to the bottom of api.js

```
// new Netlify way to start the server
const handler = serverless(app);

// we use this so the handler can use async (that mongoose uses)
module.exports.handler = async (event, context) => {
  // you can do any code here
  const result = await handler(event, context);
  // and here
  return result;
};

```

Comment out app.listen

In the terminal in server

npm i netlify-lambda serverless-http

In api.js add:

```
const serverless = require("serverless-http")

```

In package.json make sure it is mongoose 6.5

```
"mongoose": "6.5",

```

Make sure you save the package.json

Delete node_modules from the server then run npm i in the terminal.

Ensure @aws-sdk is not in the node_modules folder

In package.json replace scripts with

```
"scripts": {
    "start": "./node_modules/.bin/netlify-lambda serve src",
    "build": "./node_modules/.bin/netlify-lambda build src"
  },
```

In terminal in server Run npm start to test if the server is working
“

Deploy site in netlify

Name the site the same as the frontend but -api at the end.

Change all the API calls to 

```
`https://vans-db-api.netlify.app/.netlify/functions/api/vans`

```

Created a file in the client Called api.js

Inside enter

```
const REAL_URL = `https://vans-db-api.netlify.app/.netlify/functions/api`;
const DEV_URL = `http://localhost:9000/.netlify/functions/api`;

export const API_URL = REAL_URL;


```
In search bar search for localhost and change any entries of localhost to:

EXAMPLE: 

```
`${API_URL}/vans`

```

Make sure you import {API_URL} at the top of the file.

EXAMPLE:

```
import { API_URL } from "../../api";

```

Save all files

Open a new terminal in vs code

Git add .
Git commit -m “site deployed”
Git push
