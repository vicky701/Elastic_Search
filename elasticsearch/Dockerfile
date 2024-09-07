# base image
FROM ubuntu:20.04

# Arguments
ENV ES_JAVA_OPTS="-Xms512m -Xmx512m"
ENV ES_VERSION="7.17.5"
ENV ES_HOME="/usr/share/elasticsearch"
ENV PATH="/usr/share/elasticsearch/bin:$PATH"

# Install Java and other dependencies
RUN apt-get update && apt-get install -y wget curl openjdk-11-jdk && apt-get clean

# Create the elasticsearch user
RUN groupadd -g 1000 elasticsearch && useradd elasticsearch -u 1000 -g 1000

# Download and install Elasticsearch
RUN wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-$ES_VERSION-linux-x86_64.tar.gz --no-check-certificate && \
    tar -xzf elasticsearch-$ES_VERSION-linux-x86_64.tar.gz && \
    mv elasticsearch-$ES_VERSION $ES_HOME && \
    rm elasticsearch-$ES_VERSION-linux-x86_64.tar.gz

# Set the working directory
WORKDIR /usr/share/elasticsearch

# Set permissions for the necessary directories
RUN set -ex && for path in data logs config config/scripts; do \
    mkdir -p "$path"; \
    chown -R elasticsearch:elasticsearch "$path"; \
    done

# Copy configuration files
COPY logging.yml /usr/share/elasticsearch/config/
COPY elasticsearch.yml /usr/share/elasticsearch/config/

# Set the external JDK for Elasticsearch
ENV ES_JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64

# Switch to the elasticsearch user
USER elasticsearch

# Define the path for Elasticsearch binaries
ENV PATH=$PATH:/usr/share/elasticsearch/bin

# Run Elasticsearch
CMD ["elasticsearch"]

# Expose necessary ports
EXPOSE 9200 9300
