# @dockerfile.Template@
FROM eclipse-temurin:21.0.3_9-jre-jammy
RUN apt update && \
    apt -y --no-install-recommends --no-install-suggests install libjemalloc2 curl && \
    apt clean && rm -rf /var/lib/apt/lists/*
ENV LD_PRELOAD=/usr/lib/aarch64-linux-gnu/libjemalloc.so.2

RUN useradd -s /bin/false -U -u 20000 crashteam

COPY --chown=crashteam:crashteam ${artifactId}-${version}.jar /opt/${artifactId}/${artifactId}.jar

USER crashteam:crashteam

CMD ["java", "-jar", "/opt/${artifactId}/${artifactId}.jar"]

EXPOSE ${exposed.ports}

WORKDIR /opt/${artifactId}
