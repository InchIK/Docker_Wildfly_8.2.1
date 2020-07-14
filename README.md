**Start Docker Wildfly**  

docker run -p 8080:8080 -p 9990:9990 -it kungyc/wildfly /opt/jboss/wildfly/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0  

----------

**wildfly Admin Management**  
Dockerfile  

FROM kungyc/wildfly_8.2.1  
RUN /opt/jboss/wildfly/bin/add-user.sh admin password --silent  
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]  


**Start Docker WildflyAdmin**  

docker build --tag=kungyc/wildfly_admin .  
docker run -p 8080:8080 -p 9990:9990 -it kungyc/wildfly_admin /opt/jboss/wildfly/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0  

---------

**Deployment War File (war檔在同一個目錄下)**  
Dockerfile  

FROM kungyc/wildfly_8.2.1  
ADD system.war /opt/jboss/wildfly/standalone/deployments/  

**Start Docker WildflyAPP**  
docker build --tag=wildfly_app .  
docker run -p 8080:8080 -p 9990:9990 -it wildfly_app /opt/jboss/wildfly/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0  
