FROM alpine:latest
LABEL maintainer "Peter Sellars <psellars@gmail.com>"

RUN apk update && \
	apk upgrade && \
	apk --no-cache add bash tar curl ca-certificates && \
	apk --no-cache add --virtual wget unzip ca-certificates && \
	apk del wget unzip

ENV GIT_URL="https://github.com/npryce/adr-tools/archive/2.1.0.zip"
ENV USER=psellars
ENV USER_ID=1000
ENV USER_HOME=/home/psellars

RUN addgroup -S ${USER} -g ${USER_ID} && \
	adduser -S -G ${USER} -u ${USER_ID} -s /bin/sh -h ${USER_HOME} ${USER} 

RUN wget --no-check-certificate -O adr-tools-2.1.0.zip ${GIT_URL} && \
	unzip adr-tools-2.1.0.zip && \
	mv adr-tools-2.1.0/src /usr/local/bin/adr-tools && \
	chown -R psellars:psellars /usr/local/bin/adr-tools && \
	mkdir -p project/doc && \
	chown -R psellars:psellars project && \
	mkdir -p /usr/local/bin/adr-tools/.adr-dir && \
	chown -R psellars:psellars /usr/local/bin/adr-tools/.adr-dir

WORKDIR /project

USER ${USER}

ENTRYPOINT ["bash","/usr/local/bin/adr-tools/adr"]
