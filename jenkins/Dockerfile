FROM zbcjackson/baseimage
MAINTAINER Jackson Zhang <zbcjackson@gmail.com>

ENV JENKINS_HOME /opt/jenkins/data
ENV JENKINS_MIRROR http://mirrors.jenkins-ci.org

# install jenkins.war and plugins
RUN mkdir -p $JENKINS_HOME/plugins

RUN curl -o /opt/jenkins/jenkins.war -L $JENKINS_MIRROR/war-stable/latest/jenkins.war

RUN for plugin in scm-api git-client ansicolor git ;\
    do curl -sf -o $JENKINS_HOME/plugins/${plugin}.hpi \
           -L $JENKINS_MIRROR/plugins/${plugin}/latest/${plugin}.hpi ; done

# ADD JENKINS_HOME 
ADD JENKINS_HOME $JENKINS_HOME
RUN chmod +x $JENKINS_HOME/start.sh

EXPOSE 8080

CMD [ "/opt/jenkins/data/start.sh" ]
