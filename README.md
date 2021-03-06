# Flow API [![Circle CI](https://circleci.com/gh/srmds/Flow-API/tree/master.svg?style=shield&circle-token=46d1551fd9854de4f8ca53006186dc35aeeb6889)](https://circleci.com/gh/srmds/Flow-API/tree/master)
Rest API

[https://flow-api.herokuapp.com](https://flow-api.herokuapp.com)


## Prerequisites

[Nodejs](https://nodejs.org)

[NPM](https://www.npmjs.com)

[MongoDB](https://www.mongodb.org)


Nodejs install via brew (OSX):

[http://brew.sh](http://brew.sh)

then, install nodejs package:

    brew install node
    
## Install dependencies

NPM is used as dependencies/package manager.

To install the needed modules for this Nodejs app, 
run the following command from the `root`of the project:

    sudo npm install

Note that these dependencies are not checked in on the repo 
and thus are only available on the local machine.

## Build and Run

### Environment variables

Create a .env file in the root directory of your project. Add these environment-specific variables on new lines in the form of NAME=VALUE:

    DB_HOST=<PROJECTID>.mongolab.com
    DB_NAME=database_name
    DB_PORT=default_port
    DB_USER=username
    DB_PASSWORD=password
    NODE_ENV=development
    LOCAL_HOST=localhost
    LOCAL_DBPORT=default_port

### Import JSON sample data

Startup mongo by running:

	   mongo
	   
Create a database, named `flow`:	   

	   use flow


Sample data can be found in the [samples](https://github.com/srmds/FlowAPI/tree/master/samples) dir, import by running:

via the provided shell script, found in root:

    ./data_import.sh

or manually on each file:     

		mongoimport -d db_name -c collection_name --file filename.json --jsonArray
		
### Start server
			
Finally, from `root` of the project run:
 
     nodemon app.js 
     
Nodemon will monitor for any changes and automatically restart the server if needed. 
Open up a new browser tab and go to the follow to check if server is properly running:

[http://localhost:3000](http://localhost:3000)

## API

### Endpoints

#### Artist

Path | Method | Parameters   | Description
------------ | ------------- | ------------ | -----------
[/api/v1/artists](https://flow-api.herokuapp.com/api/v1/artists) | GET  | none | Retrieve all artists details.
[/api/v1/artists/artistId](https://flow-api.herokuapp.com/api/v1/artists/AAAA) | GET  | String, artistName | Retrieve details for a specific artist.

#### Album

Path | Method | Parameters   | Description
------------ | ------------- | ------------ | -----------
[/api/v1/albums](https://flow-api.herokuapp.com/api/v1/albums) | GET  | none | Retrieve albums details.
[/api/v1/albums/artistId](https://flow-api.herokuapp.com/api/v1/albums/AAAA) | GET  | String, artistName | Retrieve albums details for a specific artist.


#### Track

Path | Method | Parameters   | Description
------------ | ------------- | ------------ | -----------
[/api/v1/tracks](https://flow-api.herokuapp.com/api/v1/tracks) | GET  | none | Retrieve all tracks details.
[/api/v1/tracks/artistId](https://flow-api.herokuapp.com/api/v1/tracks/AAAA) | GET  | String, artistName | Retrieve all tracks details for a specific artist.
[*/api/v1/tracks/albumId/]() | GET  | String, albumName | Retrieve all tracks details for a specific album.

*Not yet implemented

#### Genre

Path | Method | Parameters   | Description
------------ | ------------- | ------------ | -----------
[/api/v1/genres](https://flow-api.herokuapp.com/api/v1/genres) | GET  | String | Retrieve all genres details.
[/api/v1/genres/genreId](https://flow-api.herokuapp.com/api/v1/genres/Alternative) | GET  | String, genreName | Retrieve details for a specific genre.




## Mocha tests

For every API endpoint there are tests, see test dir.

To run the Mocha tests, from `root` run:

      npm test
      
Note that by running tests, the local mongodb is dropped and it's collections is dropped!

Every test will create a fresh collection and runs with that collection, afterwards
the collection will again be dropped. You will have to (re)run the `data_import.sh` script, as described [here](https://github.com/srmds/FlowAPI#import-json-sample-data), to
get sample data in to the database.
      
## Deploy backend
Every change to the master branch will trigger an automatic deployment
of the backend to Heroku, after a succeeded build by the CI buildserver.

The backend is accessible via:

[https://flow-api.herokuapp.com](https://flow-api.herokuapp.com)

## MIT License
Copyright 2015 srmds

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.