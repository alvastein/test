# IAM - ONE Record Workshop

Welcome to the IAM ONE Record Workshop, in this document you will find all the instructions to run a NE:ONE Server and a NE:ONE Play instance on your personal computer.

## Prerequisites

- Download and install [Docker](https://docs.docker.com/get-docker/). Setting up an account is not required.
- For Windows and some Linux computers: download and install [Git](https://git-scm.com/downloads). Setting up an account is not required. Git is installed by default on latest versions of Mac OSX.
- Download, install [Postman](https://www.postman.com/downloads/) and create a free user account.
- Optional: use a tool like [Protegé](https://protege.stanford.edu/download/protege/4.3/installanywhere/Web_Installers/) to navigate the ontology TTL file.

## Resources
- [Data Model and Ontology Visualizer](https://aloccid-iata.github.io/ontology_visualizer/)
- [API Specification and Security](https://iata-cargo.github.io/ONE-Record/)
- [Official ONE Record Repository](https://github.com/IATA-Cargo/ONE-Record)

## Step by step guide

1) Clone this repository by running the following command on a terminal window, in a folder of your choice:
   ```bash
   git clone https://github.com/alvastein/one-record-workshop.git
   ```
2) On the terminal, switch to the directory to docker-compose:
   ```bash
   cd one-record-workshop/docker-compose
   ```
3) On the terminal, start all services with the following command:
   ```bash
   docker compose up -d
   ```
4) Wait until all containers are up and running:
   ```bash
   [+] Running 6/6
    ✔ Network docker-compose_default            Created 0.0s 
    ✔ Container docker-compose-graph-db-1       Healthy 0.0s 
    ✔ Container docker-compose-keycloak-1       Healthy 0.0s 
    ✔ Container docker-compose-ne-one-server-1  Started 0.0s 
    ✔ Container docker-compose-graph-db-setup-1 Started 0.0s
   ```
5) Try to access the ONE Record Server by  http://localhost:8080 using your favorite browser. 
   You should see a HTTP Error 401 or a blank page, because you did not authenticate yet. This confirms that the ONE Record Server is up and running.

# Overview of services

| Name | Description | Base URL / Admin UI |
|-|-|-|
| [ne-one server](https://git.openlogisticsfoundation.org/wg-digitalaircargo/ne-one) | Holds the ONE Record data and implements the API specification | http://localhost:8080 |
| [ne-one view](https://git.openlogisticsfoundation.org/wg-digitalaircargo/ne-one-view) | View all logistics objects on the ne-one-server and its data | http://localhost:3000 |
| [ne-one play](https://github.com/alvastein/neoneplay) | Create, view and update linked objects | http://localhost:3001 |
| graphdb | GraphDB database as database backend for ne-one server | http://localhost:7200 |
| keycloak | Identity provider for ne-one server to authenticate ONE Record clients and to obtain tokens for outgoing requests. <br/> **Preconfigured client_id:** neone-client<br/> **Preconfigured client_secret:** lx7ThS5aYggdsMm42BP3wMrVqKm9WpNY  | http://localhost:8989 <br/> (username/password: admin/admin)|

## Authentication
Interacting with the NE:ONE Server, through NE:ONE Play or direct API calls from a tool like Postman, requires an access token generated by a registered Identity Provider Service (IdP). In this case a local Keycloak instance has been set up as the IdP and a Client ID has been created.

We prepared a Postman collection with a few common API calls to get you up and running, including an endpoint to get an access token. Follow these steps:
1. [Postman Environment](./assets/postman/Workshop.postman_environment.json). It will open a new github page, use the download button to store a copy on your computer.
1. [Download the Postman Collection](./assets/postman/Workshop.postman_collection.json) It will open a new github page, use the download button.
2. Open Postman and import the Collection.


Follow these steps to generate a token using Postman:

This is the easiest as everything has been set up in the Postman Collection. See next section for step-by-step instructions.

### Get token directly from Keycloak
1. Access you local Keycloak instance here http://localhost:8989.
2. Login with username: Admin and password: Admin
    ![Image17](./assets/image/neone_setup.PNG)
3.  

You can get a token directly in your local instance of Keycloak
can be accessed through iuts base URL .


## Postman Collection

You can either 
You can add and edit objects directly in NE:ONE Play. You can also trigger the API endpoints with a tool like Postman, and then see the objects in NE:ONE Play.
We prepared a Postman collection with a few common API calls to get you up and running. You will need to install Postman or a compatible software in order to use it.

1. [Download the Postman Collection here.](./assets/postman/Workshop.postman_collection.json) It will open a new github page, use the download button to get the file

2. [Download the Postman Environment here](./assets/postman/Workshop.postman_environment.json). It will open a new github page, use the download button to get the file

3. Import the Environment in Postman (drag and drop file)

4. Import the Collection in Postman (drag and drop file)

5. In the Environments tab, select Workshop environment from the dropdown on the upper right corner.

6. Select Collections on the right menu and open the Workshop collection already imported

8. Use the Token Request call to generate an access token

9. Copy the access token (it might be a long string, please copy the full content) in the Authorization tab of the Get ServerInformation and run the call

10. If everything is setup correctly, you will see the server information of the AWS server

11. Copy the access token in Authentication tab of the Workshop folder

## Add NE:ONE server into NE:ONE Play

1. Connect to NE:ONE Play http://localhost:3001 

2. Click on the setting button in the top-right corner (cog icon)

3. Add your server following this instruction:

    - Organization Name: <Choose a name (any string is accepted)>
    - Protocol: http
    - Host: localhost:8080  
    - Token : <Use the postman collection to generate a token and copy it here (follow the previous paragraph)>
    - Color : pick up a random color

    ![Image17](./assets/image/neone_setup.PNG)

4. Now you can start using NE:ONE Play.

Happy data sharing!
