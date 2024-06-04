## jBPM Workbench Showcase Docker Image


**Introduction**

This image provides a ready-to-run environment for jBPM Workbench. It includes:

* JBoss Wildfly 23.0.2.Final
* jBPM Workbench 7.74.1.Final
* KIE Server 7.74.1.Final
* jBPM Case Management Showcase 7.74.1.Final

**Usage**

1. Run a container:

` docker run -p 8080:8080 -p 8001:8001 -d --name jbpm-server-full jboss/jbpm-server-full:latest`

2. After the container and web applications start, access them using a user from the "Users and Roles" section. Use the following URL:

<a href="https://brm.sherazlodhi.com/business-central" target="_blank">Business Rule Management</a>


4. The Execution server API is accessible at the URL:

<a href="https://brm.sherazlodhi.com/kie-server/docs/" target="_blank">KIE Server Documentation</a>



6. The JBPM case management is available at URL :
  
<a href="https://brm.sherazlodhi.com/jbpm-casemgmt" target="_blank">jBPM Case Management</a>


**Users and Roles**

This image includes default users and roles:

| User | Password | Role |
|---|---|---|
| wbadmin | wbadmin | admin, analyst, user, process-admin, kie-server |
| krisv | krisv | admin, analyst, user, process-admin, kie-server |
| john | john | analyst, Accounting, PM, kie-server |
| sales-rep | sales-rep | analyst, sales, kie-server |
| katy | katy | analyst, HR, kie-server |
| jack | jack | analyst, IT, kie-server |

**Database**

This image supports H2, MySQL, and PostgreSQL databases. By default, it uses H2 with file storage located at `/standalone/data/jbpm-db`. You can switch to MySQL or PostgreSQL using environment variables or Docker Compose examples.

**Docker Compose Examples**

* MySQL:

`docker-compose -f docker-compose-examples/jbpm-full-mysql.yml up`


* PostgreSQL:

`docker-compose -f docker-compose-examples/jbpm-full-postgres.yml up`


**Environment Variables**

* `JBPM_DB_DRIVER`: Database driver (h2, mysql, or postgres). Defaults to h2.
* `JBPM_DB_HOST`: Database hostname. Defaults to localhost.
* `JBPM_DB_PORT`: Database port. Defaults to 3306 (MySQL) or 5432 (PostgreSQL).
* `JBPM_DB_NAME`: Database name. Defaults to jbpm.
* `JBPM_DB_USER`: Database username. Defaults to jbpm.
* `JBPM_DB_PASSWORD`: Database password. Defaults to jbpm.

**Logging**

* View logs from the standalone binary:

`docker logs [-f] <container_id>`


* Attach to the container:

`docker attach <container_id>`


* Web application logs are located at `/opt/jboss/wildfly/standalone/log/server.log` inside the container.

**GIT Internal Repository Access**

The workbench stores projects in an internal Git repository accessible via SSH on port 8001.

**Example: Cloning the IT_Orders Sample Project**

`git clone ssh://wbadmin@localhost:8001/MySpace/IT_Orders`


**Persistent Configuration**

By default, Docker removes container data on removal. To create a persistent environment, use Docker volumes.

**Using Default GIT Root Directory**

`docker run -p 8080:8080 -p 8001:8001 -v /home/myuser/wb_git:/opt/jboss/wildfly/bin/.niogit:Z -d --name jbpm-server-full jboss/jbpm-server-full:latest`


**Custom GIT Repository Location**

Set the `-Dorg.uberfire.nio.git.dir` Java system property to your desired location.

**Environment Variables**

* `KIE_SERVER_ID`: Kie Server configuration identifier. Defaults to sample-server.
* `KIE_SERVER_LOCATION`: Kie Server public URL. Defaults to https://brm.sherazlodhi.com/kie-server/services
