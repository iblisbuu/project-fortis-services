FROM node:9.2.0

ADD . /app
ADD docker/project-fortis-services/run-server.sh /app/run-server.sh

WORKDIR /app

RUN apt-get install -y --no-install-recommends wget ca-certificates \
 && wget -q http://www-eu.apache.org/dist/cassandra/3.11.0/apache-cassandra-3.11.0-bin.tar.gz \
 && tar xfz apache-cassandra-3.11.0-bin.tar.gz \
 && rm apache-cassandra-3.11.0-bin.tar.gz \
 && mv apache-cassandra-3.11.0 /opt/cassandra \
 && npm install

ENV ENABLE_V2=1

ENV PUBLISH_EVENTS_EVENTHUB_CONNECTION_STRING="..."
ENV PUBLISH_EVENTS_EVENTHUB_PATH="..."
ENV PUBLISH_EVENTS_EVENTHUB_PARTITION="..."
ENV USER_FILES_BLOB_ACCOUNT_NAME="..."
ENV USER_FILES_BLOB_ACCOUNT_KEY="..."
ENV TRANSLATION_SERVICE_ACCOUNT_KEY="..."
ENV FACEBOOK_AUTH_TOKEN="..."
ENV APPINSIGHTS_INSTRUMENTATIONKEY="..."

# setting up the feature service is a lengthy process so we provide a shared
# instance for convenience; if you wish to run this service locally, please
# follow the instructions at https://github.com/CatalystCode/featureService and
# then update the value of this environment variable to http://localhost:3035
ENV FORTIS_FEATURE_SERVICE_HOST="http://fortis-features.eastus.cloudapp.azure.com"

ENV CASSANDRA_CONTACT_POINTS="..."
ENV CASSANDRA_KEYSPACE="fortis"
ENV CASSANDRA_USERNAME="cassandra"
ENV CASSANDRA_PASSWORD="cassandra"

ENV FORTIS_CASSANDRA_SCHEMA_URL="https://raw.githubusercontent.com/CatalystCode/fortisdeploy/master/ops/storage-ddls/cassandra-setup.cql"
ENV FORTIS_CASSANDRA_SEED_DATA_URL=""

EXPOSE 80
CMD "/app/run-server.sh"
