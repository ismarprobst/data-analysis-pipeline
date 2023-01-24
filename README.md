# data-analysis-pipeline
A short project importing a csv file through pandas to a PostgreSQL Database

On this project we will use a database about the NY yellow taxi trips. We will use the data from jan/2021

#Techs used:
- Python 3.9
- Pandas
- PostgreSQL connection library
- pscli
- pgAdmin
- PostgreSQL
- Docker
- Docker-compose

## To run this project:


You'll need Docker installed on your plataform and Docker must be running.
Before running the commands, you'll need to set a variable on the terminal. This variable will set the link where's the CSV is hosted.

You can use this script on any CSV file you want to analyse.


- First, we will dockerize our python script, creating an image of it. On terminal:

```

docker build -t taxi_ingest:v001 .

```

taxi_ingest:v001 is our image name

- Now we need to start our containers. On the project directory terminal:

```
docker-compose up
```

- Then we need to set the URL variable on the terminal:

```
URL="https://github.com/DataTalksClub/nyc-tlc-data/releases/download/yellow/yellow_tripdata_2021-01.csv.gz"
```

- Now we just run this on terminal:

```
docker run -it \
  --network=2_docker_sql_default \
  taxi_ingest:v001 \
    --user=root \
    --password=root \
    --host=pgdatabase \
    --port=5432 \
    --db=ny_taxi \
    --table_name=yellow_taxi_trips \
    --url=${URL}
```
where "network" is the docker-compose network created, then is the image name, the BDs user and password defined. Host is the service name defined on the docker-compose file.

You can check then on the pgadmin address if its working. (or pgcli on terminal)



