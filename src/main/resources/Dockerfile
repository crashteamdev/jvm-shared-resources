# @dockerfile.Template@
FROM eclipse-temurin:21-jre-jammy
RUN apt update && \
    apt -y --no-install-recommends --no-install-suggests install libjemalloc2 curl && \
    apt clean && rm -rf /var/lib/apt/lists/*
RUN ARCH=$(dpkg --print-architecture) && \
    if [ "$ARCH" = "amd64" ]; then \
        echo "export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libjemalloc.so.2" >> /etc/environment; \
    elif [ "$ARCH" = "arm64" ]; then \
        echo "export LD_PRELOAD=/usr/lib/aarch64-linux-gnu/libjemalloc.so.2" >> /etc/environment; \
    fi

RUN useradd -s /bin/false -U -u 20000 crashteam

COPY --chown=crashteam:crashteam ${artifactId}-${version}.jar /opt/${artifactId}/${artifactId}.jar

USER crashteam:crashteam

CMD ["java", "-jar", "/opt/${artifactId}/${artifactId}.jar"]

EXPOSE ${exposed.ports}

WORKDIR /opt/${artifactId}
