# STEP 2 – FRONTEND CREATION

Since we are done with the functionality we want from our backend and API, it is time to create a user interface for a Web client (browser) to interact with the application via API. To start out with the frontend of the To-do app, we will use the create-react-app command to scaffold our app.

N

1. In the same root directory as your backend code, which is the Todo directory, run:

` npx create-react-app client` 

- This will create a new folder in your Todo directory called client, where you will add all the react code. 

Note: You might run into an error if you are using a older version of node. upgrade to the latest version and retry the command if it throws and error. 

![](assets/step2-frontend/create-react-app.png)


### Running a React App

Before testing the react app, there are some dependencies that need to be installed

1. Install concurrently. It is used to run more than one command simultaneously from the same terminal window.
run `npm install concurrently --save-dev`

![](assets/step2-frontend/install-concurrently.png)

2. Install nodemon. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes

`npm install nodemon --save-dev`

![](assets/step2-frontend/install-nodemon.png)

3. In Todo folder open the package.json file. Change the highlighted part of the below screenshot and replace with the code below.

"scripts": {
"start": "node index.js",
"start-watch": "nodemon index.js",
"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
},

![](assets/step2-frontend/edit-packagejson.png)

### Configure Proxy in package.json

1. Change directory to ‘client’  `cd client`

2. Open the package.json file `vi package.json`

3. Add the key value pair in the package.json file "proxy": "http://localhost:5000".

![](assets/step2-frontend/add-proxy.png)

#### The whole purpose of adding the proxy configuration in number 3 above is to make it possible to access the application directly from the browser by simply calling the server url like http://localhost:5000 rather than always including the entire path like http://localhost:5000/api/todos

- Now, ensure you are inside the Todo directory, and simply do: `npm run dev`
- Your app should open and start running on localhost:3000
![](assets/step2-frontend/run-reactapp.png)


### Creating your React Components

One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. For our Todo app, there will be two stateful components and one stateless component
 
1. From your Todo directory run `cd client`

2. move to the src directory `cd src`

3. Inside your src folder create another folder called components `mkdir components`

4. Move into the components directory with `cd components`

5. Inside ‘components’ directory create three files Input.js, ListTodo.js and Todo.js.
`touch Input.js ListTodo.js Todo.js`

6. Open Input.js file `vi Input.js`

7. COpy and paste the following

import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {

state = {
action: ""
}

addTodo = () => {
const task = {action: this.state.action}

    if(task.action && task.action.length > 0){
      axios.post('/api/todos', task)
        .then(res => {
          if(res.data){
            this.props.getTodos();
            this.setState({action: ""})
          }
        })
        .catch(err => console.log(err))
    }else {
      console.log('input field required')
    }

}

handleChange = (e) => {
this.setState({
action: e.target.value
})
}

render() {
let { action } = this.state;
return (
<div>
<input type="text" onChange={this.handleChange} value={action} />
<button onClick={this.addTodo}>add todo</button>
</div>
)
}
}

export default Input


![](assets/step2-frontend/index-component.png)

8. To make use of Axios, which is a Promise based HTTP client for the browser and node.js, you need to cd into your client from your terminal and run yarn add axios or npm install axios.

- Move to the src folder `cd ..`
- Move to clients folder `cd ..`
- Install Axios `npm install axios`

### Now sip some coffee






