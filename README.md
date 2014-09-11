gmetad-rrdgroup-plugin
======================

A plugin for gmetad-python in ganglia to summarize monitor statistics via user-defined groups.

How to use the plugin
======================

The plugin is a derived from the RRDPlugin in gmetad-python. It works accompany with RRDPlugin to summrize the monitor statistics of all hosts in the cluster via different user-defined aggragation groups.

* Copy the plugin (rrd_group_plugin.py) into the directory gmetad-python/plugins
* Add following conf in gmetad-python.conf

<pre><code>rrdgroup {
  summary_groups "user_name"    # The type of aggregation-group, which should match with the group-attr field in redis-server
}

redis {
  redis_host "127.0.0.1"        # The location of the redis-server to store the extra group-attr of all hosts under monitor
  redis_port 6379
  redis_db   0
}
</code></pre>

* Setup a redis-server to store the group-attr of a given host. Use hash to store the group-attr of a given host. e.g:

<pre><code>redis> hset *hostKey* *group-attr* *group-attr-value*
</code></pre>

*hostKey* is the id of the host when data is retrived from gmond,<br>
*group-attr* is the group type to summarize (e.g., "user_name" in gmetad-python.conf),<br>
*group-attr-value* is the value of the group-attr of this host.
