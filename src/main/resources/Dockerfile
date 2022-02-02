# @dockerfile.Template@
FROM openjdk:17.0.2-slim

RUN useradd -s /bin/false -U -u 20000 crashteam

COPY --chown=crashteam:crashteam @artifactId@-@version@.jar /opt/@artifactId@/@artifactId@.jar

USER crashteam:crashteam

CMD ["java", "-Xmx256m", "-jar","/opt/@artifactId@/@artifactId@.jar"]

EXPOSE @exposed.ports@

WORKDIR /opt/@artifactId@
