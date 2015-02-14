docker-kibana
=============

Vagrant setup for a Kibana 4 and Elasticsearch container combo.

Spin-up
-------

~~~
$ vagrant up --no-parallel
~~~

This will first initialize a local Docker host based on Ubuntu 14.04,
install the latest Docker release and then download and initialize the two containers.

Caveat: Kibana 4 is a bit picky when Elasticsearch isn't available
immediately on launch. On the initial build, spin up may take
a little longer. In this case, the kibana container will exit.  A manual `vagrant up kibana` will fix this.

Exposed ports
-------------

This setup currently exposes `:9200` for Elasticsearch data
ingestion and `:5601` for the Kibana dashboard.

Shared folders
--------------

Elasticsearch data is stored outside of both the Docker host and the
Elasticsearch container in `host/esdata/`.
