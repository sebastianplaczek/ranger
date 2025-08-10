FROM maven:3.9.11-eclipse-temurin-8 AS base

ENV RANGER_VERSION=2.7.0 \
    MAVEN_OPTS="-Xmx4096m -XX:MaxMetaspaceSize=512m"

RUN apt-get update && \
    apt-get install -y python3-dev gcc git && \
    apt-get clean && rm -rf /var/lib/apt/lists/*


# Or you can use the binary from the official site: https://ranger.apache.org/download.html (currently no pre-built available)
RUN cd /opt \
 && git clone --depth 1 --branch release-ranger-$RANGER_VERSION https://github.com/apache/ranger.git \
 && cd ranger \
 && mvn -DskipTests -Denunciate.skip=true clean compile package install --errors --show-version -am --no-transfer-progress \
 && rm -rf ~/.m2 \
 && ls | grep -v target | xargs rm -rf \
 && rm -rf target/*.zip

ENTRYPOINT ["bash"]
