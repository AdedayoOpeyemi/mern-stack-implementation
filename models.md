# MODELS

Now comes the interesting part, since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model.

A model is at the heart of JavaScript based applications, and it is what makes it interactive.

We will also use models to define the database schema . This is important so that we will be able to define the fields stored in each Mongodb document. (Seems like a lot of information, but not to worry, everything will become clear to you over time. I promise!!!)

In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties


1. To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier.

Change directory back Todo folder with cd .. and install Mongoose. run `npm install mongoose`

![](assets/models/install-mongoose.png)

2. Create a new folder models : run `mkdir models`

3. Change directory into the newly created ‘models’ folder with `cd models`

![](assets/models/mkdir-models.png)

4. Inside the models folder, create a file and name it todo.js run `touch todo.js`

![](assets/models/touch-todojs-model.png)


#### extra: Tip: All three commands above can be defined in one line to be executed consequently with help of && operator, like this:

`mkdir models && cd models && touch todo.js`

5. Open the file created with vim todo.js then paste the code below in the file:
run `vim todo.js`
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;

![](assets/models/edit-todojs-model.png)

6. Now we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model.

In Routes directory, open api.js with vim api.js, delete the code inside with `:%d` command and paste there code below into it then save and exit

![](assets/models/edit-route-apijs.png)

### The next piece of our application will be the MongoDB Database