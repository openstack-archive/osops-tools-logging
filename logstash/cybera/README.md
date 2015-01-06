# Cybera

Example config and dashboards developed at Cybera for our public clouds. Most of the dashboards are largely to see what kind of information can be pulled from the logs or as alternatives to watching for specific log entries in a very busy `tail -f` stream.

Setup:
All services are set to DEBUG and to log to syslog, and the nodes then forward to a central rsyslog server that runs [beaver](https://github.com/josegonzalez/python-beaver) to push and tag the logs to our Rabbit cluster. The logstash agent then pulls the logs from Rabbit.

Caveats:
Beaver can only manage pushing up to 350 events/sec due to the way the Pika (Rabbit) library is used. If better performance is needed - look at the Redis options.

## Dashboards

### DefaultView.json

The Default View gives an overview of the number of logs between regions, along with some log based counts of instance creation/deletion, volume creation/deletion, and snapshot creation.

<Screenshot>

### SnapshotCheckpoints.json

Shows the "checkpoints" of instance snapshotting.

<Screenshot>

### InstanceCRUD.json

Shows instance creation and deletion along with snapshot creation points.

<Screenshot>

### Migrations.json

Shows the "checkpoints" of instance migration. One of the queries needs to be changed to the base of your compute node's fqdn. (node1.example.com would be just example.com)

<Screenshot>

### VolumeCRUD.json

Shows volume creation and deletion.

<Screenshot>

## Logstash

Logstash.conf - example downloading from rabbit.

## Beaver

beaver.conf - The example beaver config showing what we tag logs with.

