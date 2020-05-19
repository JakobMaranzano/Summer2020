# Template web app using docker containers.
Builds Docker containers (Mosquitto, Node-RED, PostgreSQL, InfluxDB, Grafana) and configures
them for a general web app.

## Overview
* *docker-compose.yml*:
  * Creates services with volumes and network
    * Mosquitto
    * Node-RED
    * PostgreSQL
    * InfluxDB
    * Grafana
* *docker_teardown.sh*
  * Removes all containers, images, volumes and networks associated with this repository

## Getting started
1. clone this repository
2. run docker-compose
`$docker-compose up -d`
3. Open browser to localhost:1880
  * In the PostgreSQL flow open the postgres node and edit the defined database.
    * Insert the user and password defined in the postgres/Dockerfile. You should
    change these if you want to deploy externally.
      * user: postgres
      * password: postgrespassword
  * Deploy the flow when done
4. Open browser to localhost:3000
  * Default username and password:
    * user: admin
    * password: grafana
  * The *Example Dashboard* demonstrates the plotting of data stored in the postgres
  and influx databases.

## Customization
1. PostgreSQL
  * Define the schema in the *postgres/create_database.sql*
  * Configure the access permissions in *postgres/pg_hba.conf*
    * Run the *docker_extra.sh*, which will copy the configuration into the proper
    location of the container
2. Influx
  * Define the databases in the *influx/database_setup.iql*
  * Configure the service in *influx/influx.conf*
3. Node-RED
  * Define new flows. The flows get coppied to */data* of the container, which
  is a named volume *node-red-data*.
  * Configure the secitury in *node-red/settings*
  * To add new nodes, log into the container and use npm:
    * docker exec -it node-red bash
    * cd /usr/src/node-red/
    * npm install *your-desired-nodes*
4. Mosquitto
  * Configure the broker in *mosquitto/mosquitto.conf*
5. Grafana
  * Create/modify dashboards. The pre-installed dashboard is in *grafana/grafana.db*,
  which gets coppied to */var/lib/grafana* within the container and is a named volume
  *grafana-data*.

# Author

**Brent Maranzano**

# License

This project is licensed under the MIT License - see the LICENSE file for details
