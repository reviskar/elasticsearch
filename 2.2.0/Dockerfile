FROM phenompeople/centos-sunjre:latest
LABEL maintainer="rene.viskar@upitech.ee  "
EXPOSE 9200 9300
ARG ELASTIC_VERSION=2.2.0
ARG ES_HOME=/usr/local/elasticsearch
RUN useradd -u 403 elasticsearch && \
	wget -q -O /tmp/elasticsearch.tar.gz https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-${ELASTIC_VERSION}.tar.gz && \
	tar -xzf /tmp/elasticsearch.tar.gz -C /usr/local && \
	chown -R elasticsearch:elasticsearch /usr/local/elasticsearch-${ELASTIC_VERSION} && \
	sed -e '/-Xmx2g/d' -e  '/-Xms2g/d' -i /usr/local/elasticsearch-${ELASTIC_VERSION}/config/jvm.options && \
	ln -sf /usr/local/elasticsearch-${ELASTIC_VERSION} ${ES_HOME}
RUN /usr/local/elasticsearch/bin/elasticsearch-plugin install analysis-icu
RUN	/usr/local/elasticsearch/bin/elasticsearch-plugin install analysis-phonetic
USER elasticsearch
ENV JAVA_HOME=/usr/local/jre \
	ES_HOME=${ES_HOME}
ENTRYPOINT ["/usr/local/elasticsearch/bin/elasticsearch"]
