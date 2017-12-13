# usage
# docker run -v /var/run/docker.sock:/var/run/docker.sock -p 5000:5000 -p 8080:8080 --privileged toninho09/jenkins-with-docker
FROM jenkins/jenkins
MAINTAINER Antonio <antoniohls@gmail.com>

USER root

RUN apt-get update \
&& apt-get -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common\
&& curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | apt-key add - \
&& apt-key fingerprint 0EBFCD88 \
&& add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") $(lsb_release -cs) stable" \
&& apt-get update \
&& apt-get -y install docker-ce \
&& apt-get -y autoremove \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* 

USER jenkins

EXPOSE 8080
EXPOSE 50000

ENTRYPOINT ["/bin/tini", "--", "/usr/local/bin/jenkins.sh"]
