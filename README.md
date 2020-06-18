# CryptoStore
A backend for stroing crypto related stats and protfolio data 
stores data in mongo db 
uses steramsets to fetch data from coinmarketcap 



## Enironment Setup 
This section describes all steps required for:		
backend - mongo install (stors pricing and other data)		
pipelines - streamsets (loads data from coinmarketcap)	 	
vm - securing firewall  streamsets and mongo	  	

### Mongo install 
link : https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
sudo apt-get install gnupg
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list

sudo apt-get update

sudo apt-get install -y mongodb-org


### Mongo after install 

use admin 
db.createUser(
  {
    user: "",
    pwd: "",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)

sudo nano /etc/mongod.conf

security:
  authorization: enabled
  

### Mongo secure access 
  sudo ufw enable
  sudo ufw allow OpenSSH
  sudo ufw allow from 91.140.122.112 to any port 27017



 sudo nano /etc/mongod.conf
 add public ip of mongo host to 
	bindIp: 127.0.0.1,IP_of_MongoHost 
  in 	
	
	
  https://stackoverflow.com/questions/23943651/mongodb-admin-user-not-authorized
db.grantRolesToUser('admin', [{ role: 'root', db: 'admin' }])
### java install 
sudo apt-get install openjdk-8-jre
### streamsets install 


wget https://archives.streamsets.com/datacollector/3.16.0/tarball/activation/streamsets-datacollector-all-3.16.0.tgz

cd /home
mkdir Downlods 
wget https://archives.streamsets.com/datacollector/3.16.0/tarball/activation/streamsets-datacollector-all-3.16.0.tgz
mkdir /opt/streamsets

cp /home/Downloads/streamsets-datacollector-all-3.16.0.tgz  /opt/streamsets
cd /opt/streamsets
tar xvzf streamsets-datacollector-all-3.16.0.tgz

[Set limits:](https://superuser.com/questions/1200539/cannot-increase-open-file-limit-past-4096-ubuntu)
   by modifying the conf file /etc/security/limits.conf
            
                *                hard    nofile          65535
                *                soft    nofile          65535
                root             soft    nofile          65535
                root             hard    nofile          65535
		

sudo ufw allow from <client_ip> to any port 18630




