# Guide to upgrade mongo to 3.2.6
## Install mongo first
1. install following two packages to unix box under /opt/ref/mongodb-3.2.6

  - mongodb-enterprise-shell-3.2.6-1.el6.x86_64.rpm
  - mongodb-enterprise-server-3.2.6-1.el6.x86_64.rpm

2. after installation done, create folder  /opt/ref/mongodb-3.2.6/config
3. cp mongo configuration to /opt/ref/mongodb-3.2.6/config
4. create db folder 
- /data/PFRefDataMongo/PFMongoCache3.2.6
- /data/PFRefDataMongo/PFMongoCache3.2.6/node1
- /data/PFRefDataMongo/PFMongoCache3.2.6/node2
4. change the user to gpfadm for folders recursively on all the servers
- /opt/ref/mongodb-3.2.6 
- /data/PFRefDataMongo/PFMongoCache3.2.6
5. test mongo connection
```sh 
    /opt/ref/mongodb-3.2.6/bin/mongo pfsvmdb1u:28018  
```
# Mongo replicate configuration
1. start mongo with auth = false and no replica settings
```sh
	/opt/ref/mongodb-3.2.6/bin/mongod --config /opt/ref/mongodb-3.2.6/config/mongod3.2.6.conf.rep1.txt
```
2. go to admin db and add root user
```sh
	use admin;
	db.createUser( { user: "root",
				 pwd: "root",
				 roles: ["root"] }
	)
```
3. can create other dbs with use command and creat users under the db
```sh
	use SMC;
	db.createCollection("Product");
	db.createUser( { user: "smc_rw",
					 pwd: "apple1",
					 roles: ["readWrite"] }
	 )
	 
	use REF;
	db.createCollection("Product");
	 db.createUser( { user: "ref_rw",
					 pwd: "apple1",
					 roles: ["readWrite"] }
	 )
```
4. restart mongo with auth = true and replica settings
5. run replicate command with the user have sufficient privilege for replicate or cluster(use root here. more details https://docs.mongodb.com/manual/core/security-built-in-roles/)
```sh
	use admin;
	db.auth("root","root");
	rs.initiate();
	rs.add("pfsvmdb1u.nam.nsroot.net:28019");
	#check the status
	rs.status();
```
6. 	reconfig replicate
```sh
	cfg = rs.conf();
	cfg.members.splice(2,1);
	rs.reconfig(cfg);
```
 
 
 
 
