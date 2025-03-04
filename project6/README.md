# FLASK API PROJECT

---

## What is an API?

---

### Definition

An API, or Application Programming Interface, is a set of rules that allows different software applications to communicate with each other. Think of it as a messenger that takes requests and tells a system what you want to do, then returns the response back to you.

### Everyday Examples

- _Weather Apps_: When you check the weather on your phone, the app sends a request to a weather service API, which then sends back the weather data.
- _Social Media Sharing_: When you share a YouTube video on Facebook, an API allows Facebook to access the YouTube video data and display it on your timeline.
- _Online Payments_: When you buy something online, an API allows the online store to communicate with your bank to process the payment.

## Why Are APIs Important?

---

### Modularity

APIs allow different parts of a software system to be developed independently. For example, a mobile app can use an API to interact with a backend server without needing to know how the server works internally.

### Scalability

APIs make it easier to scale applications. You can add more servers or services that communicate via APIs without disrupting the existing system.

### Reusability

APIs enable the reuse of code and services across different applications. For example, a payment processing API can be used by multiple e-commerce websites.

## How Do APIs Work?

---

### Basic Components

1. Request: The client (e.g., your web browser) sends a request to the server. This request usually includes:

- Endpoint: The URL where the API can be accessed.
- Method: The type of action you want to perform (e.g., GET, POST, PUT, DELETE).
- Headers: Additional information sent with the request (e.g., authentication tokens).
- Body: The data sent with the request (for methods like POST or PUT).

2. Response: The server processes the request and sends back a response. This response typically includes:

- Status Code: Indicates the result of the request (e.g., 200 for success, 404 for not found).
- Headers: Additional information about the response.
- Body: The data returned by the server (usually in JSON format).

### Example Interaction

Imagine you want to get a list of users from a server:

1. Request: Your application sends a GET request to `http://example.com/api/users`.
2. Response: The server responds with a list of users in JSON format.

```
[
  { "id": 1, "name": "Alice" },
  { "id": 2, "name": "Bob" }
]
```

## Types of APIs

---

### REST (Representational State Transfer)

- Most Common: REST APIs use standard HTTP methods (GET, POST, PUT, DELETE).
- Stateless: Each request from the client to the server must contain all the information needed to understand and process the request.

### SOAP (Simple Object Access Protocol)

- Older Protocol: Uses XML for message format and can be more complex.
- Highly Secure: Often used in enterprise-level applications where security and transaction management are crucial.

### GraphQL

- Newer Query Language: Allows clients to request exactly the data they need.
- Flexible: Reduces the amount of data transferred over the network by allowing more specific queries.

## Key Benefits of APIs

---

- Efficiency: APIs can be used to automate tasks, reducing the need for manual intervention.
- Innovation: APIs allow developers to access and integrate new technologies and services easily.
- Collaboration: Different teams can work on different parts of a system simultaneously, improving productivity and innovation.

## Learn [more](https://www.youtube.com/watch?v=ByGJQzlzxQg) about APIs

This should give you a good foundational understanding of what APIs are and why they are important.

```
flask_api_project/
├── app.py
├── templates/
│   └── index.html
├── static/
│   └── style.css
```

## Setting Up the Project

---

To create the project directory structure and set up a virtual environment, run the following commands in your VScode command line git bash or powershell:

### To open up your terminal in VScode

- Use the shortcut "Ctrl + ` " (backtick key). - Windows users
- Use the shortcut "Cmd + ` " (backtick key). - Mac user

Option 2: Click on the Terminal option in the top menu and select New Terminal.

### Use Bash for this project

---

![](./img/1.png)

### Using gitbash

---

`mkdir -p flask_api_project/{templates,static} && touch flask_api_project/app.py flask_api_project/templates/index.html flask_api_project/static/style.css && python -m venv flask_api_project/venv`
![](./img/2.png)

The command above will create the project enviroment

1. In the `app.py` file paste the code below

```
from flask import Flask, request, jsonify, render_template

app = Flask(__name__)

users = []

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/users', methods=['POST'])
def create_user():
    user = request.get_json()
    users.append(user)
    return jsonify(user), 201

@app.route('/users', methods=['GET'])
def get_users():
    return jsonify(users), 200

@app.route('/users/<int:user_id>', methods=['GET'])
def get_user(user_id):
    user = next((u for u in users if u['id'] == user_id), None)
    return jsonify(user), 200 if user else 404

@app.route('/users/<int:user_id>', methods=['PUT'])
def update_user(user_id):
    user = request.get_json()
    index = next((i for i, u in enumerate(users) if u['id'] == user_id), None)
    if index is not None:
        users[index] = user
        return jsonify(user), 200
    return '', 404

@app.route('/users/<int:user_id>', methods=['DELETE'])
def delete_user(user_id):
    global users
    users = [u for u in users if u['id'] != user_id]
    return '', 204

if __name__ == '__main__':
    app.run(debug=True)
```

2. In the `index.html` in the `templates` directory paste the code below:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>API-Based Application</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <h1>User Management</h1>
    <form id="userForm">
        <input type="text" id="name" placeholder="Name" required>
        <input type="email" id="email" placeholder="Email" required>
        <button type="submit">Add User</button>
    </form>
    <ul id="userList"></ul>

    <script>
        document.getElementById('userForm').addEventListener('submit', async function (event) {
            event.preventDefault();
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;

            const response = await fetch('/users', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ name, email })
            });

            const user = await response.json();
            document.getElementById('userList').innerHTML += `<li>${user.name} (${user.email})</li>`;
        });
    </script>
</body>
</html>
```

3. In the `style.css` in the `static` directory paste this code below there:

```
body {
    font-family: Arial, sans-serif;
    margin: 20px;
}

form {
    margin-bottom: 20px;
}

input {
    margin-right: 10px;
}
```

### Step 3: Running the Application

## Window Users

---

```
python -m venv venv
source venv/Scripts/activate
pip install Flask
```

## Mac Users

---

```
source venv/bin/activate
pip install Flask
```

Run your Flask application:

```
flask run
```

Open your browser and go to ` http://127.0.0.1:5000` to view your application.
![](./img/3.png)
![](./img/4.png)
![](./img/5.png)

## Step 4: Testing the API

### What is Postman?

Postman is a popular API development and testing tool that simplifies the process of creating, testing, documenting, and sharing APIs. It provides a user-friendly interface to make HTTP requests, set request headers, define request parameters, and handle responses. Postman can be very helpful for developers working with APIs, as it allows them to quickly test endpoints, debug issues, and automate testing. Watch this short tutorial on how to use postman [here](https://www.youtube.com/watch?v=CLG0ha_a0q8)

<table>
<tr><td>
 Installing postman
</td></tr>
<tr>
<td width="30%">
System
</td>
<td width="70%">
To Install
</td>
</tr>
<tr>
<td>Windows</td>
<td>

[Download](https://dl.pstmn.io/download/latest/win64)</td>

</tr>
<tr>
<td>Mac (Apple silicon) installation:</td>
<td>

`curl -o- "https://dl-cli.pstmn.io/install/osx_arm64.sh" | sh`

</td>
</tr>
<tr>
<td>Mac (Intel) installation</td>
<td>

`curl -o- "https://dl-cli.pstmn.io/install/osx_64.sh" | sh`</td>

</tr>
</table>

- Create a new request.
  ![](./img/6.png)

- Set the request type to `POST` and enter `http://127.0.0.1:5000/users`.

![](./img/7.png)

- Go to the `Body` tab, select `raw`, and choose `JSON` from the dropdown.

- Enter the JSON data:

```
{
    "id": 1,
    "name": "your name",
    "email": "yourname@example.com"
}
```

- Click `Send` and check the response.
  ![](./img/8.png)

## HTTP Status Codes and their meaning:

---

- 200 OK: The request was successful (common for GET, PUT).
- 201 Created: A new resource was created (common for POST).
- 204 No Content: The resource was successfully deleted (common for DELETE).
- 404 Not Found: The requested resource was not found (if you try to GET, PUT, or DELETE a non-existing user).
