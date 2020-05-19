# Template web app using docker containers.
Builds Docker containers (Mosquitto, Node-RED, PostgreSQL, InfluxDB, Grafana) and configures them for a general web app.

## Container Ports
1. localhost:1880 opens Node-Red
  * Add /ui for website
2. localhost:8888 opens jupyter notebook
3. localhost:5000 opens flask test webpage
4. localhost:3000 opens grafana database
5. localhost:8086 opens influx database

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