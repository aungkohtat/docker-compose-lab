# docker-compose-lab
## To start the application

- Step 1: Create docker network

- `docker network create mongo-network `
```bash
gitpod /workspace/docker-compose-lab (main) $ docker network ls
NETWORK ID     NAME            DRIVER    SCOPE
7c056c9c5333   bridge          bridge    local
bbf47eb94b06   host            host      local
e370b4095bd6   mongo-network   bridge    local
b079c3cbc4fe   none            null      local
gitpod /workspace/docker-compose-lab (main) $ 

- Step 2: start mongodb

- `docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo    
`

```bash
gitpod /workspace/docker-compose-lab (main) $ docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo    
Unable to find image 'mongo:latest' locally
latest: Pulling from library/mongo
a48641193673: Pull complete 
9cf348a38ee3: Pull complete 
3aa8507b7d76: Pull complete 
841ef8d499cd: Pull complete 
97788ce9e1a0: Pull complete 
194a4afa4855: Pull complete 
becfac27bfec: Pull complete 
63d2c40642ff: Pull complete 
1634c5425c04: Pull complete 
Digest: sha256:3f765972fa2d1d0a748762ba43930f06f0c3ea58986582dd4663fe5ad7b63f0e
Status: Downloaded newer image for mongo:latest
7ae5abe2af864b75482b6b6bfea69716f66be7ea6e666916368e1f45b94ae764
```

- Step 3: start mongo-express

- `docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express   
`

```bash
gitpod /workspace/docker-compose-lab (main) $ docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express   
Unable to find image 'mongo-express:latest' locally
latest: Pulling from library/mongo-express
c926b61bad3b: Pull complete 
bc7465dc4da3: Pull complete 
de7b2bf3cf64: Pull complete 
3604fe7c8f3c: Pull complete 
ef732f87d67b: Pull complete 
0e2ade824855: Pull complete 
76bb6e5f1580: Pull complete 
ee9c4596edbe: Pull complete 
Digest: sha256:def90e4f63189d3d27e04b4f44a111637723841604fbec63b5d946b96e80013d
Status: Downloaded newer image for mongo-express:latest
92d849e4d4f7a32f430d95595c8ef152b7659285c4589bccc004e0d398e2a99c
```

**NOTE: creating docker-network in optional. You can start both containers in a default network. In this case, just emit --net flag in docker run command**


## With Docker Compose
### To start the application

- Step 1: start mongodb and mongo-express
## docker compose up

```bash
gitpod /workspace/docker-compose-lab (main) $ docker compose -f docker-compose.yaml up
[+] Running 3/3
 ✔ Network docker-compose-lab_default            C...                                      0.1s 
 ✔ Container docker-compose-lab-mongodb-1        Created                                   0.0s 
 ✔ Container docker-compose-lab-mongo-express-1  Created                                   0.0s 
Attaching to mongo-express-1, mongodb-1
mongo-express-1  | Waiting for mongo:27017...
mongodb-1        | about to fork child process, waiting until server is ready for connections.
mongodb-1        | forked process: 136
mongodb-1        | 
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.229+00:00"},"s":"I",  "c":"CONTROL",  "id":20698,   "ctx":"main","msg":"***** SERVER RESTARTED *****"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.230+00:00"},"s":"I",  "c":"CONTROL",  "id":23285,   "ctx":"main","msg":"Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.231+00:00"},"s":"I",  "c":"NETWORK",  "id":4915701, "ctx":"main","msg":"Initialized wire specification","attr":{"spec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":21},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":21},"outgoing":{"minWireVersion":6,"maxWireVersion":21},"isInternalClient":true}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.233+00:00"},"s":"I",  "c":"NETWORK",  "id":4648601, "ctx":"main","msg":"Implicit TCP FastOpen unavailable. If TCP FastOpen is required, set tcpFastOpenServer, tcpFastOpenClient, and tcpFastOpenQueueSize."}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.234+00:00"},"s":"I",  "c":"REPL",     "id":5123008, "ctx":"main","msg":"Successfully registered PrimaryOnlyService","attr":{"service":"TenantMigrationDonorService","namespace":"config.tenantMigrationDonors"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.234+00:00"},"s":"I",  "c":"REPL",     "id":5123008, "ctx":"main","msg":"Successfully registered PrimaryOnlyService","attr":{"service":"TenantMigrationRecipientService","namespace":"config.tenantMigrationRecipients"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.234+00:00"},"s":"I",  "c":"CONTROL",  "id":5945603, "ctx":"main","msg":"Multi threading initialized"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.234+00:00"},"s":"I",  "c":"TENANT_M", "id":7091600, "ctx":"main","msg":"Starting TenantMigrationAccessBlockerRegistry"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.235+00:00"},"s":"I",  "c":"CONTROL",  "id":4615611, "ctx":"initandlisten","msg":"MongoDB starting","attr":{"pid":136,"port":27017,"dbPath":"/data/db","architecture":"64-bit","host":"56582a4ffa2e"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.235+00:00"},"s":"I",  "c":"CONTROL",  "id":23403,   "ctx":"initandlisten","msg":"Build Info","attr":{"buildInfo":{"version":"7.0.5","gitVersion":"7809d71e84e314b497f282ea8aa06d7ded3eb205","openSSLVersion":"OpenSSL 3.0.2 15 Mar 2022","modules":[],"allocator":"tcmalloc","environment":{"distmod":"ubuntu2204","distarch":"x86_64","target_arch":"x86_64"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.235+00:00"},"s":"I",  "c":"CONTROL",  "id":51765,   "ctx":"initandlisten","msg":"Operating System","attr":{"os":{"name":"Ubuntu","version":"22.04"}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.235+00:00"},"s":"I",  "c":"CONTROL",  "id":21951,   "ctx":"initandlisten","msg":"Options set by command line","attr":{"options":{"net":{"bindIp":"127.0.0.1","port":27017,"tls":{"mode":"disabled"}},"processManagement":{"fork":true,"pidFilePath":"/tmp/docker-entrypoint-temp-mongod.pid"},"systemLog":{"destination":"file","logAppend":true,"path":"/proc/1/fd/1"}}}}
mongo-express-1  | /docker-entrypoint.sh: line 15: mongo: Name does not resolve
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.237+00:00"},"s":"I",  "c":"STORAGE",  "id":22315,   "ctx":"initandlisten","msg":"Opening WiredTiger","attr":{"config":"create,cache_size=31637M,session_max=33000,eviction=(threads_min=4,threads_max=4),config_base=false,statistics=(fast),log=(enabled=true,remove=true,path=journal,compressor=snappy),builtin_extension_config=(zstd=(compression_level=6)),file_manager=(close_idle_time=600,close_scan_interval=10,close_handle_minimum=2000),statistics_log=(wait=0),json_output=(error,message),verbose=[recovery_progress:1,checkpoint_progress:1,compact_progress:1,backup:0,checkpoint:0,compact:0,evict:0,history_store:0,recovery:0,rts:0,salvage:0,tiered:0,timestamp:0,transaction:0,verify:0,log:0],"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.391+00:00"},"s":"I",  "c":"STORAGE",  "id":4795906, "ctx":"initandlisten","msg":"WiredTiger opened","attr":{"durationMillis":154}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.391+00:00"},"s":"I",  "c":"RECOVERY", "id":23987,   "ctx":"initandlisten","msg":"WiredTiger recoveryTimestamp","attr":{"recoveryTimestamp":{"$timestamp":{"t":0,"i":0}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.396+00:00"},"s":"W",  "c":"CONTROL",  "id":22120,   "ctx":"initandlisten","msg":"Access control is not enabled for the database. Read and write access to data and configuration is unrestricted","tags":["startupWarnings"]}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.396+00:00"},"s":"W",  "c":"CONTROL",  "id":5123300, "ctx":"initandlisten","msg":"vm.max_map_count is too low","attr":{"currentValue":65530,"recommendedMinimum":1677720,"maxConns":838860},"tags":["startupWarnings"]}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.397+00:00"},"s":"I",  "c":"STORAGE",  "id":20320,   "ctx":"initandlisten","msg":"createCollection","attr":{"namespace":"admin.system.version","uuidDisposition":"provided","uuid":{"uuid":{"$uuid":"fda9178f-3cc6-4503-9643-9913495639e5"}},"options":{"uuid":{"$uuid":"fda9178f-3cc6-4503-9643-9913495639e5"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.401+00:00"},"s":"I",  "c":"INDEX",    "id":20345,   "ctx":"initandlisten","msg":"Index build: done building","attr":{"buildUUID":null,"collectionUUID":{"uuid":{"$uuid":"fda9178f-3cc6-4503-9643-9913495639e5"}},"namespace":"admin.system.version","index":"_id_","ident":"index-1--7078916906425488781","collectionIdent":"collection-0--7078916906425488781","commitTimestamp":null}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.401+00:00"},"s":"I",  "c":"REPL",     "id":20459,   "ctx":"initandlisten","msg":"Setting featureCompatibilityVersion","attr":{"newVersion":"7.0"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.401+00:00"},"s":"I",  "c":"REPL",     "id":5853300, "ctx":"initandlisten","msg":"current featureCompatibilityVersion value","attr":{"featureCompatibilityVersion":"7.0","context":"setFCV"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.401+00:00"},"s":"I",  "c":"NETWORK",  "id":4915702, "ctx":"initandlisten","msg":"Updated wire specification","attr":{"oldSpec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":21},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":21},"outgoing":{"minWireVersion":6,"maxWireVersion":21},"isInternalClient":true},"newSpec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":21},"incomingInternalClient":{"minWireVersion":21,"maxWireVersion":21},"outgoing":{"minWireVersion":21,"maxWireVersion":21},"isInternalClient":true}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.401+00:00"},"s":"I",  "c":"NETWORK",  "id":4915702, "ctx":"initandlisten","msg":"Updated wire specification","attr":{"oldSpec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":21},"incomingInternalClient":{"minWireVersion":21,"maxWireVersion":21},"outgoing":{"minWireVersion":21,"maxWireVersion":21},"isInternalClient":true},"newSpec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":21},"incomingInternalClient":{"minWireVersion":21,"maxWireVersion":21},"outgoing":{"minWireVersion":21,"maxWireVersion":21},"isInternalClient":true}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.401+00:00"},"s":"I",  "c":"REPL",     "id":5853300, "ctx":"initandlisten","msg":"current featureCompatibilityVersion value","attr":{"featureCompatibilityVersion":"7.0","context":"startup"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.401+00:00"},"s":"I",  "c":"STORAGE",  "id":5071100, "ctx":"initandlisten","msg":"Clearing temp directory"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.402+00:00"},"s":"I",  "c":"CONTROL",  "id":6608200, "ctx":"initandlisten","msg":"Initializing cluster server parameters from disk"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.402+00:00"},"s":"I",  "c":"CONTROL",  "id":20536,   "ctx":"initandlisten","msg":"Flow Control is enabled on this deployment"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.402+00:00"},"s":"I",  "c":"FTDC",     "id":20625,   "ctx":"initandlisten","msg":"Initializing full-time diagnostic data capture","attr":{"dataDirectory":"/data/db/diagnostic.data"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.403+00:00"},"s":"I",  "c":"STORAGE",  "id":20320,   "ctx":"initandlisten","msg":"createCollection","attr":{"namespace":"local.startup_log","uuidDisposition":"generated","uuid":{"uuid":{"$uuid":"7dce9872-fcd3-4b49-8d69-2f7652b761ce"}},"options":{"capped":true,"size":10485760}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.408+00:00"},"s":"I",  "c":"INDEX",    "id":20345,   "ctx":"initandlisten","msg":"Index build: done building","attr":{"buildUUID":null,"collectionUUID":{"uuid":{"$uuid":"7dce9872-fcd3-4b49-8d69-2f7652b761ce"}},"namespace":"local.startup_log","index":"_id_","ident":"index-3--7078916906425488781","collectionIdent":"collection-2--7078916906425488781","commitTimestamp":null}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.408+00:00"},"s":"I",  "c":"REPL",     "id":6015317, "ctx":"initandlisten","msg":"Setting new configuration state","attr":{"newState":"ConfigReplicationDisabled","oldState":"ConfigPreStart"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.408+00:00"},"s":"I",  "c":"STORAGE",  "id":22262,   "ctx":"initandlisten","msg":"Timestamp monitor starting"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.409+00:00"},"s":"I",  "c":"NETWORK",  "id":23015,   "ctx":"listener","msg":"Listening on","attr":{"address":"/tmp/mongodb-27017.sock"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.409+00:00"},"s":"I",  "c":"NETWORK",  "id":23015,   "ctx":"listener","msg":"Listening on","attr":{"address":"127.0.0.1"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.409+00:00"},"s":"I",  "c":"NETWORK",  "id":23016,   "ctx":"listener","msg":"Waiting for connections","attr":{"port":27017,"ssl":"off"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.409+00:00"},"s":"I",  "c":"CONTROL",  "id":20712,   "ctx":"LogicalSessionCacheReap","msg":"Sessions collection is not set up; waiting until next sessions reap interval","attr":{"error":"NamespaceNotFound: config.system.sessions does not exist"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.409+00:00"},"s":"I",  "c":"CONTROL",  "id":8423403, "ctx":"initandlisten","msg":"mongod startup complete","attr":{"Summary of time elapsed":{"Startup from clean shutdown?":true,"Statistics":{"Transport layer setup":"0 ms","Run initial syncer crash recovery":"0 ms","Create storage engine lock file in the data directory":"0 ms","Get metadata describing storage engine":"0 ms","Create storage engine":"159 ms","Write current PID to file":"0 ms","Write a new metadata for storage engine":"0 ms","Initialize FCV before rebuilding indexes":"0 ms","Drop abandoned idents and get back indexes that need to be rebuilt or builds that need to be restarted":"0 ms","Rebuild indexes for collections":"0 ms","Load cluster parameters from disk for a standalone":"1 ms","Build user and roles graph":"0 ms","Set up the background thread pool responsible for waiting for opTimes to be majority committed":"0 ms","Initialize information needed to make a mongod instance shard aware":"0 ms","Start up the replication coordinator":"0 ms","Start transport layer":"0 ms","_initAndListen total elapsed time":"174 ms"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.410+00:00"},"s":"I",  "c":"STORAGE",  "id":20320,   "ctx":"LogicalSessionCacheRefresh","msg":"createCollection","attr":{"namespace":"config.system.sessions","uuidDisposition":"generated","uuid":{"uuid":{"$uuid":"673dc67f-dfa1-4bce-9488-87b8620fb67e"}},"options":{}}}
mongodb-1        | child process started successfully, parent exiting
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.414+00:00"},"s":"I",  "c":"REPL",     "id":7360102, "ctx":"LogicalSessionCacheRefresh","msg":"Added oplog entry for create to transaction","attr":{"namespace":"config.$cmd","uuid":{"uuid":{"$uuid":"673dc67f-dfa1-4bce-9488-87b8620fb67e"}},"object":{"create":"system.sessions","idIndex":{"v":2,"key":{"_id":1},"name":"_id_"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.414+00:00"},"s":"I",  "c":"REPL",     "id":7360100, "ctx":"LogicalSessionCacheRefresh","msg":"Added oplog entry for createIndexes to transaction","attr":{"namespace":"config.$cmd","uuid":{"uuid":{"$uuid":"673dc67f-dfa1-4bce-9488-87b8620fb67e"}},"object":{"createIndexes":"system.sessions","v":2,"key":{"lastUse":1},"name":"lsidTTLIndex","expireAfterSeconds":1800}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.416+00:00"},"s":"I",  "c":"INDEX",    "id":20345,   "ctx":"LogicalSessionCacheRefresh","msg":"Index build: done building","attr":{"buildUUID":null,"collectionUUID":{"uuid":{"$uuid":"673dc67f-dfa1-4bce-9488-87b8620fb67e"}},"namespace":"config.system.sessions","index":"_id_","ident":"index-5--7078916906425488781","collectionIdent":"collection-4--7078916906425488781","commitTimestamp":null}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.416+00:00"},"s":"I",  "c":"INDEX",    "id":20345,   "ctx":"LogicalSessionCacheRefresh","msg":"Index build: done building","attr":{"buildUUID":null,"collectionUUID":{"uuid":{"$uuid":"673dc67f-dfa1-4bce-9488-87b8620fb67e"}},"namespace":"config.system.sessions","index":"lsidTTLIndex","ident":"index-6--7078916906425488781","collectionIdent":"collection-4--7078916906425488781","commitTimestamp":null}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.794+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"127.0.0.1:33560","uuid":{"uuid":{"$uuid":"b2403688-9643-44a3-ae09-621debef41dc"}},"connectionId":1,"connectionCount":1}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.801+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn1","msg":"client metadata","attr":{"remote":"127.0.0.1:33560","client":"conn1","doc":{"application":{"name":"mongosh 2.1.1"},"driver":{"name":"nodejs|mongosh","version":"6.3.0|2.1.1"},"platform":"Node.js v20.9.0, LE","os":{"name":"linux","architecture":"x64","version":"6.1.66-060166-generic","type":"Linux"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.813+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"127.0.0.1:33572","uuid":{"uuid":{"$uuid":"a1bb2206-91f8-4e74-8f30-184b56797b4f"}},"connectionId":2,"connectionCount":2}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.813+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"127.0.0.1:33582","uuid":{"uuid":{"$uuid":"a9631305-5fe2-4866-bb9b-3b9821b048d2"}},"connectionId":3,"connectionCount":3}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.814+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn2","msg":"client metadata","attr":{"remote":"127.0.0.1:33572","client":"conn2","doc":{"application":{"name":"mongosh 2.1.1"},"driver":{"name":"nodejs|mongosh","version":"6.3.0|2.1.1"},"platform":"Node.js v20.9.0, LE","os":{"name":"linux","architecture":"x64","version":"6.1.66-060166-generic","type":"Linux"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.814+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn3","msg":"client metadata","attr":{"remote":"127.0.0.1:33582","client":"conn3","doc":{"application":{"name":"mongosh 2.1.1"},"driver":{"name":"nodejs|mongosh","version":"6.3.0|2.1.1"},"platform":"Node.js v20.9.0, LE","os":{"name":"linux","architecture":"x64","version":"6.1.66-060166-generic","type":"Linux"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.816+00:00"},"s":"I",  "c":"NETWORK",  "id":6788700, "ctx":"conn2","msg":"Received first command on ingress connection since session start or auth handshake","attr":{"elapsedMillis":2}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.817+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"127.0.0.1:33590","uuid":{"uuid":{"$uuid":"cfa1e9e7-74d0-492b-9c22-21349e9e8ab6"}},"connectionId":4,"connectionCount":4}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.820+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn4","msg":"client metadata","attr":{"remote":"127.0.0.1:33590","client":"conn4","doc":{"application":{"name":"mongosh 2.1.1"},"driver":{"name":"nodejs|mongosh","version":"6.3.0|2.1.1"},"platform":"Node.js v20.9.0, LE","os":{"name":"linux","architecture":"x64","version":"6.1.66-060166-generic","type":"Linux"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:44.821+00:00"},"s":"I",  "c":"NETWORK",  "id":6788700, "ctx":"conn4","msg":"Received first command on ingress connection since session start or auth handshake","attr":{"elapsedMillis":1}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.047+00:00"},"s":"I",  "c":"NETWORK",  "id":22944,   "ctx":"conn1","msg":"Connection ended","attr":{"remote":"127.0.0.1:33560","uuid":{"uuid":{"$uuid":"b2403688-9643-44a3-ae09-621debef41dc"}},"connectionId":1,"connectionCount":3}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.047+00:00"},"s":"I",  "c":"NETWORK",  "id":22944,   "ctx":"conn4","msg":"Connection ended","attr":{"remote":"127.0.0.1:33590","uuid":{"uuid":{"$uuid":"cfa1e9e7-74d0-492b-9c22-21349e9e8ab6"}},"connectionId":4,"connectionCount":2}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.048+00:00"},"s":"I",  "c":"NETWORK",  "id":22944,   "ctx":"conn3","msg":"Connection ended","attr":{"remote":"127.0.0.1:33582","uuid":{"uuid":{"$uuid":"a9631305-5fe2-4866-bb9b-3b9821b048d2"}},"connectionId":3,"connectionCount":1}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.048+00:00"},"s":"I",  "c":"NETWORK",  "id":22944,   "ctx":"conn2","msg":"Connection ended","attr":{"remote":"127.0.0.1:33572","uuid":{"uuid":{"$uuid":"a1bb2206-91f8-4e74-8f30-184b56797b4f"}},"connectionId":2,"connectionCount":0}}
mongo-express-1  | Sat Jan 13 10:40:45 UTC 2024 retrying to connect to mongo:27017 (2/10)
mongo-express-1  | /docker-entrypoint.sh: line 15: mongo: Name does not resolve
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.491+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"127.0.0.1:33596","uuid":{"uuid":{"$uuid":"b94c5483-c968-45e6-a260-96935f07a2da"}},"connectionId":5,"connectionCount":1}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.495+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn5","msg":"client metadata","attr":{"remote":"127.0.0.1:33596","client":"conn5","doc":{"application":{"name":"mongosh 2.1.1"},"driver":{"name":"nodejs|mongosh","version":"6.3.0|2.1.1"},"platform":"Node.js v20.9.0, LE","os":{"name":"linux","architecture":"x64","version":"6.1.66-060166-generic","type":"Linux"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.507+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"127.0.0.1:33600","uuid":{"uuid":{"$uuid":"4f20d9f0-0664-4207-87b9-b7f2d6660973"}},"connectionId":6,"connectionCount":2}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.507+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"127.0.0.1:33606","uuid":{"uuid":{"$uuid":"a21b1a54-888a-4b70-861f-d8dd04af33b4"}},"connectionId":7,"connectionCount":3}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.508+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn6","msg":"client metadata","attr":{"remote":"127.0.0.1:33600","client":"conn6","doc":{"application":{"name":"mongosh 2.1.1"},"driver":{"name":"nodejs|mongosh","version":"6.3.0|2.1.1"},"platform":"Node.js v20.9.0, LE","os":{"name":"linux","architecture":"x64","version":"6.1.66-060166-generic","type":"Linux"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.509+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn7","msg":"client metadata","attr":{"remote":"127.0.0.1:33606","client":"conn7","doc":{"application":{"name":"mongosh 2.1.1"},"driver":{"name":"nodejs|mongosh","version":"6.3.0|2.1.1"},"platform":"Node.js v20.9.0, LE","os":{"name":"linux","architecture":"x64","version":"6.1.66-060166-generic","type":"Linux"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.511+00:00"},"s":"I",  "c":"NETWORK",  "id":6788700, "ctx":"conn6","msg":"Received first command on ingress connection since session start or auth handshake","attr":{"elapsedMillis":2}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.511+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"127.0.0.1:33608","uuid":{"uuid":{"$uuid":"a9ec0ede-4664-42c7-8c3a-d8a6080e8e91"}},"connectionId":8,"connectionCount":4}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.514+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn8","msg":"client metadata","attr":{"remote":"127.0.0.1:33608","client":"conn8","doc":{"application":{"name":"mongosh 2.1.1"},"driver":{"name":"nodejs|mongosh","version":"6.3.0|2.1.1"},"platform":"Node.js v20.9.0, LE","os":{"name":"linux","architecture":"x64","version":"6.1.66-060166-generic","type":"Linux"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.515+00:00"},"s":"I",  "c":"NETWORK",  "id":6788700, "ctx":"conn8","msg":"Received first command on ingress connection since session start or auth handshake","attr":{"elapsedMillis":1}}
mongodb-1        | admin> ... ... ... ... {"t":{"$date":"2024-01-13T10:40:45.817+00:00"},"s":"I",  "c":"STORAGE",  "id":20320,   "ctx":"conn8","msg":"createCollection","attr":{"namespace":"admin.system.users","uuidDisposition":"generated","uuid":{"uuid":{"$uuid":"3db351f4-2075-4487-95e1-a3712f5ab6d3"}},"options":{}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.822+00:00"},"s":"I",  "c":"REPL",     "id":7360102, "ctx":"conn8","msg":"Added oplog entry for create to transaction","attr":{"namespace":"admin.$cmd","uuid":{"uuid":{"$uuid":"3db351f4-2075-4487-95e1-a3712f5ab6d3"}},"object":{"create":"system.users","idIndex":{"v":2,"key":{"_id":1},"name":"_id_"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.822+00:00"},"s":"I",  "c":"REPL",     "id":7360100, "ctx":"conn8","msg":"Added oplog entry for createIndexes to transaction","attr":{"namespace":"admin.$cmd","uuid":{"uuid":{"$uuid":"3db351f4-2075-4487-95e1-a3712f5ab6d3"}},"object":{"createIndexes":"system.users","name":"user_1_db_1","key":{"user":1,"db":1},"unique":true,"v":2}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.824+00:00"},"s":"I",  "c":"INDEX",    "id":20345,   "ctx":"conn8","msg":"Index build: done building","attr":{"buildUUID":null,"collectionUUID":{"uuid":{"$uuid":"3db351f4-2075-4487-95e1-a3712f5ab6d3"}},"namespace":"admin.system.users","index":"_id_","ident":"index-8--7078916906425488781","collectionIdent":"collection-7--7078916906425488781","commitTimestamp":null}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.824+00:00"},"s":"I",  "c":"INDEX",    "id":20345,   "ctx":"conn8","msg":"Index build: done building","attr":{"buildUUID":null,"collectionUUID":{"uuid":{"$uuid":"3db351f4-2075-4487-95e1-a3712f5ab6d3"}},"namespace":"admin.system.users","index":"user_1_db_1","ident":"index-9--7078916906425488781","collectionIdent":"collection-7--7078916906425488781","commitTimestamp":null}}
mongodb-1        | { ok: 1 }
mongodb-1        | admin> {"t":{"$date":"2024-01-13T10:40:45.834+00:00"},"s":"I",  "c":"NETWORK",  "id":22944,   "ctx":"conn5","msg":"Connection ended","attr":{"remote":"127.0.0.1:33596","uuid":{"uuid":{"$uuid":"b94c5483-c968-45e6-a260-96935f07a2da"}},"connectionId":5,"connectionCount":3}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.834+00:00"},"s":"I",  "c":"NETWORK",  "id":22944,   "ctx":"conn8","msg":"Connection ended","attr":{"remote":"127.0.0.1:33608","uuid":{"uuid":{"$uuid":"a9ec0ede-4664-42c7-8c3a-d8a6080e8e91"}},"connectionId":8,"connectionCount":2}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.834+00:00"},"s":"I",  "c":"NETWORK",  "id":22944,   "ctx":"conn7","msg":"Connection ended","attr":{"remote":"127.0.0.1:33606","uuid":{"uuid":{"$uuid":"a21b1a54-888a-4b70-861f-d8dd04af33b4"}},"connectionId":7,"connectionCount":1}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.835+00:00"},"s":"I",  "c":"NETWORK",  "id":22944,   "ctx":"conn6","msg":"Connection ended","attr":{"remote":"127.0.0.1:33600","uuid":{"uuid":{"$uuid":"4f20d9f0-0664-4207-87b9-b7f2d6660973"}},"connectionId":6,"connectionCount":0}}
mongodb-1        | 
mongodb-1        | /usr/local/bin/docker-entrypoint.sh: ignoring /docker-entrypoint-initdb.d/*
mongodb-1        | 
mongodb-1        | 
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.871+00:00"},"s":"I",  "c":"CONTROL",  "id":20698,   "ctx":"main","msg":"***** SERVER RESTARTED *****"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.871+00:00"},"s":"I",  "c":"CONTROL",  "id":23285,   "ctx":"main","msg":"Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.873+00:00"},"s":"I",  "c":"NETWORK",  "id":4915701, "ctx":"main","msg":"Initialized wire specification","attr":{"spec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":21},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":21},"outgoing":{"minWireVersion":6,"maxWireVersion":21},"isInternalClient":true}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.874+00:00"},"s":"I",  "c":"NETWORK",  "id":4648601, "ctx":"main","msg":"Implicit TCP FastOpen unavailable. If TCP FastOpen is required, set tcpFastOpenServer, tcpFastOpenClient, and tcpFastOpenQueueSize."}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.874+00:00"},"s":"I",  "c":"REPL",     "id":5123008, "ctx":"main","msg":"Successfully registered PrimaryOnlyService","attr":{"service":"TenantMigrationDonorService","namespace":"config.tenantMigrationDonors"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.874+00:00"},"s":"I",  "c":"REPL",     "id":5123008, "ctx":"main","msg":"Successfully registered PrimaryOnlyService","attr":{"service":"TenantMigrationRecipientService","namespace":"config.tenantMigrationRecipients"}}
mongodb-1        | Killing process with pid: 136
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.875+00:00"},"s":"I",  "c":"CONTROL",  "id":23377,   "ctx":"SignalHandler","msg":"Received signal","attr":{"signal":15,"error":"Terminated"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.875+00:00"},"s":"I",  "c":"CONTROL",  "id":23378,   "ctx":"SignalHandler","msg":"Signal was sent by kill(2)","attr":{"pid":215,"uid":999}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.875+00:00"},"s":"I",  "c":"CONTROL",  "id":23381,   "ctx":"SignalHandler","msg":"will terminate after current cmd ends"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.875+00:00"},"s":"I",  "c":"REPL",     "id":4784900, "ctx":"SignalHandler","msg":"Stepping down the ReplicationCoordinator for shutdown","attr":{"waitTimeMillis":15000}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.875+00:00"},"s":"I",  "c":"REPL",     "id":4794602, "ctx":"SignalHandler","msg":"Attempting to enter quiesce mode"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.875+00:00"},"s":"I",  "c":"-",        "id":6371601, "ctx":"SignalHandler","msg":"Shutting down the FLE Crud thread pool"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.875+00:00"},"s":"I",  "c":"COMMAND",  "id":4784901, "ctx":"SignalHandler","msg":"Shutting down the MirrorMaestro"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.875+00:00"},"s":"I",  "c":"SHARDING", "id":4784902, "ctx":"SignalHandler","msg":"Shutting down the WaitForMajorityService"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.875+00:00"},"s":"I",  "c":"CONTROL",  "id":4784903, "ctx":"SignalHandler","msg":"Shutting down the LogicalSessionCache"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"NETWORK",  "id":20562,   "ctx":"SignalHandler","msg":"Shutdown: going to close listening sockets"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"NETWORK",  "id":23017,   "ctx":"listener","msg":"removing socket file","attr":{"path":"/tmp/mongodb-27017.sock"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"NETWORK",  "id":4784905, "ctx":"SignalHandler","msg":"Shutting down the global connection pool"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"CONTROL",  "id":4784906, "ctx":"SignalHandler","msg":"Shutting down the FlowControlTicketholder"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"-",        "id":20520,   "ctx":"SignalHandler","msg":"Stopping further Flow Control ticket acquisitions."}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"CONTROL",  "id":4784908, "ctx":"SignalHandler","msg":"Shutting down the PeriodicThreadToAbortExpiredTransactions"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"REPL",     "id":4784909, "ctx":"SignalHandler","msg":"Shutting down the ReplicationCoordinator"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"SHARDING", "id":4784910, "ctx":"SignalHandler","msg":"Shutting down the ShardingInitializationMongoD"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"REPL",     "id":4784911, "ctx":"SignalHandler","msg":"Enqueuing the ReplicationStateTransitionLock for shutdown"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"-",        "id":4784912, "ctx":"SignalHandler","msg":"Killing all operations for shutdown"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"-",        "id":4695300, "ctx":"SignalHandler","msg":"Interrupted all currently running operations","attr":{"opsKilled":3}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"TENANT_M", "id":5093807, "ctx":"SignalHandler","msg":"Shutting down all TenantMigrationAccessBlockers on global shutdown"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"ASIO",     "id":22582,   "ctx":"TenantMigrationBlockerNet","msg":"Killing all outstanding egress activity."}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"ASIO",     "id":6529201, "ctx":"SignalHandler","msg":"Network interface redundant shutdown","attr":{"state":"Stopped"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"ASIO",     "id":22582,   "ctx":"SignalHandler","msg":"Killing all outstanding egress activity."}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"COMMAND",  "id":4784913, "ctx":"SignalHandler","msg":"Shutting down all open transactions"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"REPL",     "id":4784914, "ctx":"SignalHandler","msg":"Acquiring the ReplicationStateTransitionLock for shutdown"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"INDEX",    "id":4784915, "ctx":"SignalHandler","msg":"Shutting down the IndexBuildsCoordinator"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"NETWORK",  "id":4784918, "ctx":"SignalHandler","msg":"Shutting down the ReplicaSetMonitor"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.876+00:00"},"s":"I",  "c":"SHARDING", "id":4784921, "ctx":"SignalHandler","msg":"Shutting down the MigrationUtilExecutor"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"ASIO",     "id":22582,   "ctx":"MigrationUtil-TaskExecutor","msg":"Killing all outstanding egress activity."}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"COMMAND",  "id":4784923, "ctx":"SignalHandler","msg":"Shutting down the ServiceEntryPoint"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"CONTROL",  "id":4784927, "ctx":"SignalHandler","msg":"Shutting down the HealthLog"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"CONTROL",  "id":4784928, "ctx":"SignalHandler","msg":"Shutting down the TTL monitor"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"INDEX",    "id":3684100, "ctx":"SignalHandler","msg":"Shutting down TTL collection monitor thread"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"INDEX",    "id":3684101, "ctx":"SignalHandler","msg":"Finished shutting down TTL collection monitor thread"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"CONTROL",  "id":6278511, "ctx":"SignalHandler","msg":"Shutting down the Change Stream Expired Pre-images Remover"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"CONTROL",  "id":4784929, "ctx":"SignalHandler","msg":"Acquiring the global lock for shutdown"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"CONTROL",  "id":4784930, "ctx":"SignalHandler","msg":"Shutting down the storage engine"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"STORAGE",  "id":22320,   "ctx":"SignalHandler","msg":"Shutting down journal flusher thread"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"STORAGE",  "id":22321,   "ctx":"SignalHandler","msg":"Finished shutting down journal flusher thread"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"STORAGE",  "id":22322,   "ctx":"SignalHandler","msg":"Shutting down checkpoint thread"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"STORAGE",  "id":22323,   "ctx":"SignalHandler","msg":"Finished shutting down checkpoint thread"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"STORAGE",  "id":22261,   "ctx":"SignalHandler","msg":"Timestamp monitor shutting down"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.877+00:00"},"s":"I",  "c":"STORAGE",  "id":20282,   "ctx":"SignalHandler","msg":"Deregistering all the collections"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.878+00:00"},"s":"I",  "c":"STORAGE",  "id":22317,   "ctx":"SignalHandler","msg":"WiredTigerKVEngine shutting down"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.878+00:00"},"s":"I",  "c":"STORAGE",  "id":22318,   "ctx":"SignalHandler","msg":"Shutting down session sweeper thread"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.878+00:00"},"s":"I",  "c":"STORAGE",  "id":22319,   "ctx":"SignalHandler","msg":"Finished shutting down session sweeper thread"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.878+00:00"},"s":"I",  "c":"STORAGE",  "id":4795902, "ctx":"SignalHandler","msg":"Closing WiredTiger","attr":{"closeConfig":"leak_memory=true,use_timestamp=false,"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.887+00:00"},"s":"I",  "c":"STORAGE",  "id":4795901, "ctx":"SignalHandler","msg":"WiredTiger closed","attr":{"durationMillis":9}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.887+00:00"},"s":"I",  "c":"STORAGE",  "id":22279,   "ctx":"SignalHandler","msg":"shutdown: removing fs lock..."}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.887+00:00"},"s":"I",  "c":"-",        "id":4784931, "ctx":"SignalHandler","msg":"Dropping the scope cache for shutdown"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.887+00:00"},"s":"I",  "c":"FTDC",     "id":20626,   "ctx":"SignalHandler","msg":"Shutting down full-time diagnostic data capture"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.890+00:00"},"s":"I",  "c":"CONTROL",  "id":20565,   "ctx":"SignalHandler","msg":"Now exiting"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.890+00:00"},"s":"I",  "c":"CONTROL",  "id":8423404, "ctx":"SignalHandler","msg":"mongod shutdown complete","attr":{"Summary of time elapsed":{"Statistics":{"Enter terminal shutdown":"0 ms","Step down the replication coordinator for shutdown":"0 ms","Time spent in quiesce mode":"0 ms","Shut down FLE Crud subsystem":"0 ms","Shut down MirrorMaestro":"0 ms","Shut down WaitForMajorityService":"0 ms","Shut down the logical session cache":"0 ms","Shut down the transport layer":"1 ms","Shut down the global connection pool":"0 ms","Shut down the flow control ticket holder":"0 ms","Kill all operations for shutdown":"0 ms","Shut down all tenant migration access blockers on global shutdown":"0 ms","Shut down all open transactions":"0 ms","Acquire the RSTL for shutdown":"0 ms","Shut down the IndexBuildsCoordinator and wait for index builds to finish":"0 ms","Shut down the replica set monitor":"0 ms","Shut down the migration util executor":"1 ms","Shut down the health log":"0 ms","Shut down the TTL monitor":"0 ms","Shut down expired pre-images and documents removers":"0 ms","Shut down the storage engine":"10 ms","Wait for the oplog cap maintainer thread to stop":"0 ms","Shut down full-time data capture":"0 ms","shutdownTask total elapsed time":"15 ms"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:45.890+00:00"},"s":"I",  "c":"CONTROL",  "id":23138,   "ctx":"SignalHandler","msg":"Shutting down","attr":{"exitCode":0}}
mongo-express-1  | Sat Jan 13 10:40:46 UTC 2024 retrying to connect to mongo:27017 (3/10)
mongo-express-1  | /docker-entrypoint.sh: line 15: mongo: Name does not resolve
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
mongodb-1        | 
mongodb-1        | MongoDB init process complete; ready for start up.
mongodb-1        | 
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.907+00:00"},"s":"I",  "c":"NETWORK",  "id":4915701, "ctx":"main","msg":"Initialized wire specification","attr":{"spec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":21},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":21},"outgoing":{"minWireVersion":6,"maxWireVersion":21},"isInternalClient":true}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.907+00:00"},"s":"I",  "c":"CONTROL",  "id":23285,   "ctx":"main","msg":"Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.907+00:00"},"s":"I",  "c":"NETWORK",  "id":4648601, "ctx":"main","msg":"Implicit TCP FastOpen unavailable. If TCP FastOpen is required, set tcpFastOpenServer, tcpFastOpenClient, and tcpFastOpenQueueSize."}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.908+00:00"},"s":"I",  "c":"REPL",     "id":5123008, "ctx":"main","msg":"Successfully registered PrimaryOnlyService","attr":{"service":"TenantMigrationDonorService","namespace":"config.tenantMigrationDonors"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.908+00:00"},"s":"I",  "c":"REPL",     "id":5123008, "ctx":"main","msg":"Successfully registered PrimaryOnlyService","attr":{"service":"TenantMigrationRecipientService","namespace":"config.tenantMigrationRecipients"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.908+00:00"},"s":"I",  "c":"CONTROL",  "id":5945603, "ctx":"main","msg":"Multi threading initialized"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.908+00:00"},"s":"I",  "c":"TENANT_M", "id":7091600, "ctx":"main","msg":"Starting TenantMigrationAccessBlockerRegistry"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.909+00:00"},"s":"I",  "c":"CONTROL",  "id":4615611, "ctx":"initandlisten","msg":"MongoDB starting","attr":{"pid":1,"port":27017,"dbPath":"/data/db","architecture":"64-bit","host":"56582a4ffa2e"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.909+00:00"},"s":"I",  "c":"CONTROL",  "id":23403,   "ctx":"initandlisten","msg":"Build Info","attr":{"buildInfo":{"version":"7.0.5","gitVersion":"7809d71e84e314b497f282ea8aa06d7ded3eb205","openSSLVersion":"OpenSSL 3.0.2 15 Mar 2022","modules":[],"allocator":"tcmalloc","environment":{"distmod":"ubuntu2204","distarch":"x86_64","target_arch":"x86_64"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.909+00:00"},"s":"I",  "c":"CONTROL",  "id":51765,   "ctx":"initandlisten","msg":"Operating System","attr":{"os":{"name":"Ubuntu","version":"22.04"}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.909+00:00"},"s":"I",  "c":"CONTROL",  "id":21951,   "ctx":"initandlisten","msg":"Options set by command line","attr":{"options":{"net":{"bindIp":"*"},"security":{"authorization":"enabled"}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.910+00:00"},"s":"I",  "c":"STORAGE",  "id":22270,   "ctx":"initandlisten","msg":"Storage engine to use detected by data files","attr":{"dbpath":"/data/db","storageEngine":"wiredTiger"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:46.910+00:00"},"s":"I",  "c":"STORAGE",  "id":22315,   "ctx":"initandlisten","msg":"Opening WiredTiger","attr":{"config":"create,cache_size=31637M,session_max=33000,eviction=(threads_min=4,threads_max=4),config_base=false,statistics=(fast),log=(enabled=true,remove=true,path=journal,compressor=snappy),builtin_extension_config=(zstd=(compression_level=6)),file_manager=(close_idle_time=600,close_scan_interval=10,close_handle_minimum=2000),statistics_log=(wait=0),json_output=(error,message),verbose=[recovery_progress:1,checkpoint_progress:1,compact_progress:1,backup:0,checkpoint:0,compact:0,evict:0,history_store:0,recovery:0,rts:0,salvage:0,tiered:0,timestamp:0,transaction:0,verify:0,log:0],"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.247+00:00"},"s":"I",  "c":"STORAGE",  "id":4795906, "ctx":"initandlisten","msg":"WiredTiger opened","attr":{"durationMillis":337}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.247+00:00"},"s":"I",  "c":"RECOVERY", "id":23987,   "ctx":"initandlisten","msg":"WiredTiger recoveryTimestamp","attr":{"recoveryTimestamp":{"$timestamp":{"t":0,"i":0}}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.251+00:00"},"s":"W",  "c":"CONTROL",  "id":5123300, "ctx":"initandlisten","msg":"vm.max_map_count is too low","attr":{"currentValue":65530,"recommendedMinimum":1677720,"maxConns":838860},"tags":["startupWarnings"]}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.253+00:00"},"s":"I",  "c":"NETWORK",  "id":4915702, "ctx":"initandlisten","msg":"Updated wire specification","attr":{"oldSpec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":21},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":21},"outgoing":{"minWireVersion":6,"maxWireVersion":21},"isInternalClient":true},"newSpec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":21},"incomingInternalClient":{"minWireVersion":21,"maxWireVersion":21},"outgoing":{"minWireVersion":21,"maxWireVersion":21},"isInternalClient":true}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.253+00:00"},"s":"I",  "c":"REPL",     "id":5853300, "ctx":"initandlisten","msg":"current featureCompatibilityVersion value","attr":{"featureCompatibilityVersion":"7.0","context":"startup"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.253+00:00"},"s":"I",  "c":"STORAGE",  "id":5071100, "ctx":"initandlisten","msg":"Clearing temp directory"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.254+00:00"},"s":"I",  "c":"CONTROL",  "id":6608200, "ctx":"initandlisten","msg":"Initializing cluster server parameters from disk"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.254+00:00"},"s":"I",  "c":"CONTROL",  "id":20536,   "ctx":"initandlisten","msg":"Flow Control is enabled on this deployment"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.254+00:00"},"s":"I",  "c":"FTDC",     "id":20625,   "ctx":"initandlisten","msg":"Initializing full-time diagnostic data capture","attr":{"dataDirectory":"/data/db/diagnostic.data"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.258+00:00"},"s":"I",  "c":"REPL",     "id":6015317, "ctx":"initandlisten","msg":"Setting new configuration state","attr":{"newState":"ConfigReplicationDisabled","oldState":"ConfigPreStart"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.258+00:00"},"s":"I",  "c":"STORAGE",  "id":22262,   "ctx":"initandlisten","msg":"Timestamp monitor starting"}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.259+00:00"},"s":"I",  "c":"NETWORK",  "id":23015,   "ctx":"listener","msg":"Listening on","attr":{"address":"/tmp/mongodb-27017.sock"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.259+00:00"},"s":"I",  "c":"NETWORK",  "id":23015,   "ctx":"listener","msg":"Listening on","attr":{"address":"0.0.0.0"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.259+00:00"},"s":"I",  "c":"NETWORK",  "id":23016,   "ctx":"listener","msg":"Waiting for connections","attr":{"port":27017,"ssl":"off"}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:47.259+00:00"},"s":"I",  "c":"CONTROL",  "id":8423403, "ctx":"initandlisten","msg":"mongod startup complete","attr":{"Summary of time elapsed":{"Startup from clean shutdown?":true,"Statistics":{"Transport layer setup":"0 ms","Run initial syncer crash recovery":"0 ms","Create storage engine lock file in the data directory":"0 ms","Get metadata describing storage engine":"0 ms","Validate options in metadata against current startup options":"0 ms","Create storage engine":"338 ms","Write current PID to file":"0 ms","Initialize FCV before rebuilding indexes":"2 ms","Drop abandoned idents and get back indexes that need to be rebuilt or builds that need to be restarted":"0 ms","Rebuild indexes for collections":"0 ms","Load cluster parameters from disk for a standalone":"0 ms","Build user and roles graph":"0 ms","Verify indexes for admin.system.users collection":"0 ms","Set up the background thread pool responsible for waiting for opTimes to be majority committed":"0 ms","Initialize information needed to make a mongod instance shard aware":"0 ms","Start up the replication coordinator":"0 ms","Start transport layer":"0 ms","_initAndListen total elapsed time":"350 ms"}}}}
mongo-express-1  | Sat Jan 13 10:40:47 UTC 2024 retrying to connect to mongo:27017 (4/10)
mongo-express-1  | /docker-entrypoint.sh: line 15: mongo: Name does not resolve
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
mongo-express-1  | Sat Jan 13 10:40:48 UTC 2024 retrying to connect to mongo:27017 (5/10)
mongo-express-1  | /docker-entrypoint.sh: line 15: mongo: Name does not resolve
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
mongo-express-1  | Sat Jan 13 10:40:49 UTC 2024 retrying to connect to mongo:27017 (6/10)
mongo-express-1  | /docker-entrypoint.sh: line 15: mongo: Name does not resolve
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
mongo-express-1  | Sat Jan 13 10:40:50 UTC 2024 retrying to connect to mongo:27017 (7/10)
mongo-express-1  | /docker-entrypoint.sh: line 15: mongo: Name does not resolve
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
mongo-express-1  | Sat Jan 13 10:40:51 UTC 2024 retrying to connect to mongo:27017 (8/10)
mongo-express-1  | /docker-entrypoint.sh: line 15: mongo: Name does not resolve
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
mongo-express-1  | Sat Jan 13 10:40:52 UTC 2024 retrying to connect to mongo:27017 (9/10)
mongo-express-1  | /docker-entrypoint.sh: line 15: mongo: Name does not resolve
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
mongo-express-1  | Sat Jan 13 10:40:53 UTC 2024 retrying to connect to mongo:27017 (10/10)
mongo-express-1  | /docker-entrypoint.sh: line 15: mongo: Name does not resolve
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
mongo-express-1  | No custom config.js found, loading config.default.js
mongo-express-1  | Welcome to mongo-express 1.0.2
mongo-express-1  | ------------------------
mongo-express-1  | 
mongo-express-1  | 
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:54.385+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"172.19.0.2:44590","uuid":{"uuid":{"$uuid":"1269f65d-6362-4fb4-bbe9-d0bfd858a805"}},"connectionId":1,"connectionCount":1}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:54.392+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn1","msg":"client metadata","attr":{"remote":"172.19.0.2:44590","client":"conn1","doc":{"driver":{"name":"nodejs","version":"4.13.0"},"os":{"type":"Linux","name":"linux","architecture":"x64","version":"6.1.66-060166-generic"},"platform":"Node.js v18.19.0, LE (unified)|Node.js v18.19.0, LE (unified)"}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:54.398+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"172.19.0.2:44602","uuid":{"uuid":{"$uuid":"2425b167-8f4d-45bd-a350-7e0a7007a1b2"}},"connectionId":2,"connectionCount":2}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:54.399+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn2","msg":"client metadata","attr":{"remote":"172.19.0.2:44602","client":"conn2","doc":{"driver":{"name":"nodejs","version":"4.13.0"},"os":{"type":"Linux","name":"linux","architecture":"x64","version":"6.1.66-060166-generic"},"platform":"Node.js v18.19.0, LE (unified)|Node.js v18.19.0, LE (unified)"}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:54.401+00:00"},"s":"I",  "c":"ACCESS",   "id":6788604, "ctx":"conn2","msg":"Auth metrics report","attr":{"metric":"acquireUser","micros":0}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:54.410+00:00"},"s":"I",  "c":"ACCESS",   "id":5286306, "ctx":"conn2","msg":"Successfully authenticated","attr":{"client":"172.19.0.2:44602","isSpeculative":true,"isClusterMember":false,"mechanism":"SCRAM-SHA-256","user":"admin","db":"admin","result":0,"metrics":{"conversation_duration":{"micros":9195,"summary":{"0":{"step":1,"step_total":2,"duration_micros":64},"1":{"step":2,"step_total":2,"duration_micros":26}}}},"extraInfo":{}}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:40:54.412+00:00"},"s":"I",  "c":"NETWORK",  "id":6788700, "ctx":"conn2","msg":"Received first command on ingress connection since session start or auth handshake","attr":{"elapsedMillis":1}}
mongo-express-1  | Mongo Express server listening at http://0.0.0.0:8081
mongo-express-1  | Server is open to allow connections from anyone (0.0.0.0)
mongo-express-1  | Basic authentication is disabled. It is recommended to set the useBasicAuth to true in the config.js.
mongodb-1        | {"t":{"$date":"2024-01-13T10:41:04.900+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"172.19.0.2:32796","uuid":{"uuid":{"$uuid":"944d0ed0-f358-44b9-b883-dce46c77321c"}},"connectionId":3,"connectionCount":3}}
mongodb-1        | {"t":{"$date":"2024-01-13T10:41:04.901+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn3","msg":"client metadata","attr":{"remote":"172.19.0.2:32796","client":"conn3","doc":{"driver":{"name":"nodejs","version":"4.13.0"},"os":{"type":"Linux","name":"linux","architecture":"x64","version":"6.1.66-060166-generic"},"platform":"Node.js v18.19.0, LE (unified)|Node.js v18.19.0, LE (unified)"}}}
```


```bash
gitpod /workspace/docker-compose-lab (main) $ docker compose -f docker-compose.yaml up -d
[+] Running 2/2
 ✔ Container docker-compose-lab-mongodb-1        Started                                                                        0.0s 
 ✔ Container docker-compose-lab-mongo-express-1  Started                                                                        0.0s 
gitpod /workspace/docker-compose-lab (main) $ 
```

```bash

gitpod /workspace/docker-compose-lab (main) $ docker compose -f docker-compose.yaml down
[+] Running 3/3
 ✔ Container docker-compose-lab-mongo-express-1  Removed                                                                        0.3s 
 ✔ Container docker-compose-lab-mongodb-1        Removed                                                                        0.3s 
 ✔ Network docker-compose-lab_default            Removed                                                                        0.4s 
gitpod /workspace/docker-compose-lab (main) $ 
```

```bash
gitpod /workspace/docker-compose-lab (main) $ docker compose -f docker-compose.yaml up -d
[+] Running 3/3
 ✔ Network docker-compose-lab_default            Created                                                                        0.2s 
 ✔ Container docker-compose-lab-mongodb-1        Started                                                                        0.0s 
 ✔ Container docker-compose-lab-mongo-express-1  Started                                                                        0.0s 
gitpod /workspace/docker-compose-lab (main) $ docker compose -f docker-compose.yaml stop
[+] Stopping 2/2
 ✔ Container docker-compose-lab-mongo-express-1  Stopped                                                                        0.3s 
 ✔ Container docker-compose-lab-mongodb-1        Stopped                                                                        0.3s 
gitpod /workspace/docker-compose-lab (main) $ 
```


