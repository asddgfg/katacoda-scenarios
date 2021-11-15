# 1.1 Basics
clone Eat API from GitHub repository and enther the repository folder
`git clone https://github.com/Ethan7102/COMP3122-Project.git`{{execute}}
`cd COMP3122-Project`{{execute}}

Build the docker images using the Dockerfile in the folders.
`docker-compose up`{{execute}}

Check the built images
`docker images`{{execute}}

Check the lauched  containers
`docker ps`{{execute}}

# 1.2 Get token
try the command as follows and check the response.
`curl -X POST -v http://localhost:5000/order -H 'Content-Type: application/json' -d @./order_service/sample_order_data.json`{{execute}}