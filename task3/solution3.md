<pre>
The ReplcationNotRunning alert fires when 
mysql_slave_status_slave_io_running or  mysql_slave_status_slave_sql_running
replication's metrics monitored by Prometheus return value '0'
for over 2 minutes

As I understand, IO parameter's '0' value means that replica doesn't have communication with the master due to: 
-connectivity/netowrk issues
-DNS issues 
-authentication issues
-or other issues preventing the replica from receiving data/commands. 

Speaking of mysql_slave_status_slave_sql_running,
based on Mysql Docs https://dev.mysql.com/doc/refman/8.4/en/show-replica-status.html
seems to be related to:
 Replica_SQL_Running
-Whether the replication SQL (applier) thread is started. 

As I see, it tells whether the slave can apply commands received from Master.

-

To achieve building a Grafana dashboard I decied to test with a local installation: 
Found out it requires helm - K8's deployment and configuration tool
Used it to install Prometheus and Grafana
Both tools access is acheived through port forwarding on localhost.

I did not dive in installing/setting up a MySQL instance for some demo data, just focused on using 
the metrics mentioned in the initial task:
mysql_slave_status_slave_io_running
mysql_slave_status_slave_sql_running

AI also suggested mysql_slave_status_seconds_behind_master - to display the replication lag 
which would show how many second the slave fals behind applying commands from the master.

All of these are added as spearate dashboard panels, with Prometheus set as the source of data.

The dashboard shows these 3 parameters, allowing to view the history and time how long the incident is ongoing.
Each of the parameter's value helps us understand better where to look at first for further investigation of the incident.
For example if IO parameter is triggering the alert, we may start looking straight into related possible causes instead of 
paniking and bindly looking for everything we can think of.
</pre>
