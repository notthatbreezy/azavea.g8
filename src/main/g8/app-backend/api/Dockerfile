FROM openjdk:11-jre-slim

RUN \
      addgroup --system $api_user$ \
      && adduser --system --disabled-login --disabled-password --home /var/lib/$api_user$ --shell /sbin/nologin --ingroup $api_user$ $api_user$

COPY ./target/scala-2.11/$name;format="norm"$-api-assembly.jar /var/lib/$api_user$/

USER $api_user$
WORKDIR /var/lib/$api_user$

ENTRYPOINT ["java"]
CMD ["-jar", "$name;format="norm"$-api-assembly.jar"]
