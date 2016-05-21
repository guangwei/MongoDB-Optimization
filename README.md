构建MongoDB 集群

mongodb/bin/mongod  --dbpath=/home/runner/tools/mongodb/db1 --logpath=/home/runner/tools/mongodb/db1/m.log  --fork  --replSet  replset1  --bind_ip 192.168.1.1  --port 1008 --directoryperdb --nohttpinterface  

mongodb/bin/mongod  --dbpath=/home/runner/tools/mongodb/db2 --logpath=/home/runner/tools/mongodb/db2/m.log  --fork --replSet  replset1   --bind_ip 192.168.1.2  --port 1009 --directoryperdb --nohttpinterface 

mongodb/bin/mongod  --dbpath=/home/runner/tools/mongodb/db3 --logpath=/home/runner/tools/mongodb/db3/m.log  --fork --replSet  replset1   --bind_ip 192.168.1.3  --port 1000 --directoryperdb --nohttpinterface  


链接其中一个   bin/mongo --host 192.168.1.1 --port 1008

config_replset1 = {
_id:"replset1",
members:
[
{_id:0,host:"192.168.1.1:1008",priority:4},
{_id:1,host:"192.168.1.2:1009",priority:2},
{_id:2,host:"192.168.1.3:1000",arbiterOnly : true}
]
}

rs.initiate(config_replset1);
