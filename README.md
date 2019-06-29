# CMDBuild 3 in Docker

### CMDBuild

[CMDBuild](http://www.cmdbuild.org/en) is a web environment in which you can configure custom solutions for IT Governance, or more generally for asset management.

![cmdbuild_logo](http://www.cmdbuild.org/logo.png)

### Information
This is the unofficial repository with all the versions of cmdbuild.  
I will update the repository every time there is a new version of cmdbuild available

### Deploy by docker run
CMDbuild with demo database
```bash
docker run --name cmdbuild_db -p 5432:5432 -d itmicus/cmdbuild:db-3.0
docker run --name cmdbuild_app --link cmdbuild_db  -p 8090:8080 -d itmicus/cmdbuild:app-3.0
```

CMDbuild Ready2use
```bash
docker run --name cmdbuild_db -p 5432:5432 -d itmicus/cmdbuild:db-3.0
docker run --name cmdbuild_app -e CMDBUILD_DUMP="ready2use.dump.xz" --link cmdbuild_db  -p 8090:8080 -d itmicus/cmdbuild:app-3.0
```

### Deploy by docker-compose
**CMDbuild with demo database**
```bash
git clone https://github.com/itmicus/cmdbuild_docker
docker-compose up -d
```
waiting while all container starting (about 5 minutes) and open your browser  

http://localhost:8090/cmdbuild  
**Login**: admin  
**Password**: admin  

**CMDbuild Ready2use**
Open file .env and change to CMDBUILD_DUMP=ready2use.dump.xz and save file
```bash
docker-compose up -d
```
waiting while all container starting (about 5 minutes) and open your browser  

http://localhost:8090/cmdbuild  
**Login**: admin  
**Password**: admin  



#### How drop database
If you want change type of DB you must drop old database
```bash
docker-compose exec cmdbuild_app /usr/local/tomcat/webapps/cmdbuild/cmdbuild.sh dbconfig drop -configfile /usr/local/tomcat/conf/cmdbuild/database.conf
```
and after run container with new value of CMDBUILD_DUMP

#### Tomcat
http://localhost:8090/  
**Login**: admin  
**Password**: password  

#### The default cmdbuild_app environment in the image is:

CMDBUILD_URL: https://sourceforge.net/projects/cmdbuild/files/3.0/cmdbuild-3.0.war/download  
POSTGRES_USER: postgres  
POSTGRES_PASS: postgres  
POSTGRES_PORT: 5432  
POSTGRES_HOST: cmdbuild_db  
POSTGRES_DB: cmdbuild_db30  
CMDBUILD_DUMP: demo  

#### CMDBUILD_DUMP values
* demo
* ready2use.dump.xz

### Please open issues on [github](https://github.com/itmicus/cmdbuild_docker/issues)