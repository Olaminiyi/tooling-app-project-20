FROM mysql:latest
LABEL "Project"="tooling"
LABEL "Author"="Olaminiyi"
LABEL "Description"="Building the tooling app"

ENV MYSQL_ROOT_PASSWORD="ola"

ADD create_user.sql docker-entrypoint-initdb.d/create_user.sql
ADD tooling_db_schema.sql docker-entrypoint-initdb.d/tooling_db_schema.sql
