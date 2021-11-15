# 1.1 Basics
clone Eat API from GitHub repository and enther the repository folder

`git clone https://github.com/Ethan7102/COMP3122-Project.git`{{execute}}

`cd COMP3122-Project`{{execute}}

Build the docker images using the Dockerfile in the folders

`docker-compose up`{{execute}}

Check the built images

`docker images`{{execute}}

Check the lauched containers

`docker ps`{{execute}}

# 1.2 Register token
Assume all clients have their own accounts on the service server. They can register a token using the account. For testing, a default account was created as follows.
- username: comp3122
- password: comp3122

Register a token

`curl -X POST -v http://localhost:5000/authentication/get_token -H 'Content-Type: application/json' -d '{"username":"comp3122", "password": "comp3122"}'`{{execute}}

Try the command as follows and check the response

`curl -X POST -v http://localhost:5000/order -H 'Content-Type: application/json' -d @./order_service/sample_order_data.json`{{execute}}

The permission depied 