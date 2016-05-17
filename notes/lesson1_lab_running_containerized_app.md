
# Project 1: Using Docker to Set Up a Development Environment Locally

We've set up a project so that you can see how easy Docker makes set-up for someone new to your code base.
Below we'll walk you through the steps of getting your first Docker environment up and running. 
After each step, we'll let you know if you did it right and that it's safe to move onto the next one. 

## Run docker applicaiton with one command `docker-compose up`

* From your terminal window, create and go to your project directory under your home directory.

`$ mkdir ~/sit`

`$ cd ~/sit`

* Clone the GitHub Repo (or download and extract the code) [here](link/for/the/future).

`$ git clone https://github.com/wheelhouseio/Foodtrucks`

* Use the command line to navigate to the Foodtrucks working directory.

`$ cd Foodtrucks`

* Run your Foodtrucks applicaiton in detached mode. (First time running this, it may take some time to download container images.
)

`$ docker-compose up -d`

* HINT: starts the containers in the background and leaves them running. 

`
Options:
    -d                         Detached mode: Run containers in the background,
                               print new container names.
                               Incompatible with --abort-on-container-exit.

`

* Verify that two docker containers are started and running 

`$ docker ps -a`. 

* You should see 2 containers running, elasticsearch and foodtruck-web.

## Start a browser on your laptop and navigate to [http://localhost:5000](http://localhost:5000) to perform search.
*  In your browser, go to `localhost:5000`
*  Verify the Foodtruck applicaiton is running correctly, by performing a search for "Tacos" or "Burges" etc, and find location of Foodtrucks. 
*  Navigate maps by scrolling up and down, zooming in and out, and mouse over to a particluar location for more detail informations.


## Edit code in your local machine(or training container), see it instantly changed on foodtruck-web container by sharing user volume

* Now, let's change color of the banner to purple color instead of yellow. 
* From your laptop terminal window (or Learning container depending on how you set up), go to the Foodtruck project directory. 
* Change CSS in flask-app/static/styles/main.css file. For example, change heading color from to `#ac39fd`

```
html, body { padding: 0; color: #ac39fd; box-sizing: border-box; font-family: 'Titillium Web', sans-serif; margin: 0;) }
```

* Verify the changes you have made are reflected on Foodtruck application, by refresh your browser to [http://localhost:5000](http://localhost:5000)
* The change should show up instantly. 


## Verify sharing of volume between applicaiton container and your local machine (or training container).

* Goto foodtrucks-web container `docker exec -i -t <container ID for foodtrucks-web>`
* Check the volume is created `docker volume ls`
* Check the network is created `docker network ls`
* Verify volume /opt is mounted in foodtrucks-web container same volume as from training container as a local directory by
inspecting docker container `docker inspect <container ID for foodtrucks-web>`


## Cleanup 

* Run `docker compose down` and go back to [http://localhost:5000](http://localhost:5000). Check that he application is no longer running. 
* Check `docker ps`. The containers should be stopped.

