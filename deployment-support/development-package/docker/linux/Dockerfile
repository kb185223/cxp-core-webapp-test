FROM  tomcat:9.0.37-jdk8-corretto

LABEL maintainer="SA230976@ncr.com"

# NOTE: This can be improved by picking up all the files from Artifactory, passing the version as docker cmd argument.

# In order to create the docker images, all the following files are required under the same folder as the docker file.
#
# cxp-core-webapp.war
# cxp-security-grouping-client.war
# cxp-terminal-import-client.war
# cxp-terminal-management-client.war
# cxpusermanagement-client.war
# logback.xml
#
# NOTE: If some portlets are not required, then the copy command for that portlet should be removed or commented.
# Keep in mind, that the context of the portlet registration needs to update to the right URL. 

# ncr folder containing cxp.properties, default-dashboard-config.xml, cxp.sqlserver.properties, dataload folder and
#    logs folder needs to mounted to the container while running. 
# Structure of ncr folder should be
# - ncr
#     - logs
#     - dataload
#         - <all dataload files>
#     - license
#         - licensev4.dat
#     - cxp.properties
#     - cxp.sqlserver.properties
#     - default-dashboard-config.xml
#
# It should be mounted to the container's internal folder "/mnt/ncr".
# logs location can be changed in logback.xml
#  
# Example run command:   docker run -v C:\ncr:/mnt/ncr -p 8080:8080 <image_name>

# 


# Copying all the wars into Tomcat webapps.
COPY cxp-core-webapp.war /usr/local/tomcat/webapps/
COPY cxp-security-grouping-client.war /usr/local/tomcat/webapps/
COPY cxp-terminal-import-client.war /usr/local/tomcat/webapps/
COPY cxp-terminal-management-client.war /usr/local/tomcat/webapps/
COPY cxpusermanagement-client.war /usr/local/tomcat/webapps/

# Adding logback.xml into the Tomcat Lib
COPY logback.xml /usr/local/tomcat/lib/

# Setting env variables.
ENV CXP_ENCRYPTION_ALGORITHM=PBEWITHSHA1ANDDESEDE
ENV CXP_ENCRYPTION_PASSWORD=nep
ENV com.ncr.cxp.config.location=/mnt/ncr
ENV com.ncr.cxp.terminals.license.location=/mnt/ncr/license

EXPOSE 8080

CMD ["catalina.sh", "run"]
