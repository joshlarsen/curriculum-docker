# Project 3: Running applicaiton with docker-compse 

## Write a compose file
  * Create `docker-compose.yml` file from your favorite text editor, for example;
  ` $ vi docker-compose.yml `

  * Edit the following items in `docker-compose.yml` file
    + Defining services for elasticsearch image
    + Defining foodtruck-web from your docker images
        + Calling the starting applicaiton command
        + Opening port mappings
        + Mounting volumes 
        + Linking images together so they can communicate

```

    es:
        image: elasticsearch

    web:
        image: foodtrucks-web
        command: python app.py
        ports:
             - "5000:5000"
        volumes:
             - .:/opt
        links:
             - es

```
  
  * Validate compose yaml file with yaml validator

## Run compose-up, verify the containers are running.

  * Run composed applicaiton in detached mode (Run containers in the background)

    `docker-compose up -d`

  * Check docker two containers are running

    `docker ps -a`



## Start a browser on your laptop and navigate to [http://localhost:5000](http://localhost:5000) to perform search.

-  In your browser, go to `localhost:5000`

-  Verify the Foodtruck applicaiton is running correctly, by performing a search for "Tacos" or "Burges" etc, and find location of Foodtrucks. 

-  Navigate maps by scrolling up and down, zooming in and out, and mouse over to a particluar location for more detail informations.

