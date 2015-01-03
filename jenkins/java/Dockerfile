FROM zbcjackson/jenkins
MAINTAINER Jackson Zhang <zbcjackson@gmail.com>

# get maven 3.2.2
RUN curl -o /tmp/apache-maven-3.2.2.tar.gz http://archive.apache.org/dist/maven/maven-3/3.2.2/binaries/apache-maven-3.2.2-bin.tar.gz

# install maven
RUN tar xzf /tmp/apache-maven-3.2.2.tar.gz -C /opt/
RUN ln -s /opt/apache-maven-3.2.2 /opt/maven
RUN ln -s /opt/maven/bin/mvn /usr/local/bin
RUN rm -f /tmp/apache-maven-3.2.2.tar.gz
ENV MAVEN_HOME /opt/maven


# set shell variables for java installation
ENV java_version 1.8.0_11
ENV filename jdk-8u11-linux-x64.tar.gz
ENV downloadlink http://download.oracle.com/otn-pub/java/jdk/8u11-b12/$filename

# download java, accepting the license agreement
RUN curl -L -b "oraclelicense=a" http://download.oracle.com/otn-pub/java/jdk/8u11-b12/jdk-8u11-linux-x64.tar.gz -o /tmp/$filename

# unpack java
RUN mkdir /opt/java-oracle && tar -zxf /tmp/$filename -C /opt/java-oracle/
ENV JAVA_HOME /opt/java-oracle/jdk$java_version
ENV PATH $JAVA_HOME/bin:$PATH

# configure symbolic links for the java and javac executables
RUN update-alternatives --install /usr/bin/java java $JAVA_HOME/bin/java 20000 && update-alternatives --install /usr/bin/javac javac $JAVA_HOME/bin/javac 20000
