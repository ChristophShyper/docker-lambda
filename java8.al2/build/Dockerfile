﻿FROM lambci/lambda-base-2:build

ENV PATH=/var/lang/bin:$PATH \
    LD_LIBRARY_PATH=/var/lang/lib:$LD_LIBRARY_PATH \
    AWS_EXECUTION_ENV=AWS_Lambda_rapid

RUN rm -rf /var/runtime && \
  curl https://lambci.s3.amazonaws.com/fs/java8.al2.tgz | tar -zx -C / && \
  rm -rf /var/lang/* && \
  curl -sSL https://corretto.aws/downloads/resources/8.252.09.1/amazon-corretto-8.252.09.1-linux-x64.tar.gz | tar -xz --strip-components=1 -C /var/lang && \
  rm -rf /var/lang/*.zip && \
  mkdir /usr/local/gradle && curl -L -o gradle.zip https://services.gradle.org/distributions/gradle-6.6.1-bin.zip && \
  unzip -qd /usr/local/gradle gradle.zip && rm gradle.zip && mkdir /usr/local/maven && \
  curl -L http://mirror.cc.columbia.edu/pub/software/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz | \
  tar -zx -C /usr/local/maven

ENV PATH="/usr/local/gradle/gradle-6.6.1/bin:/usr/local/maven/apache-maven-3.6.3/bin:${PATH}"

# Add these as a separate layer as they get updated frequently
RUN pipx install awscli==1.* && \
  pipx install aws-lambda-builders==1.0.0 && \
  pipx install aws-sam-cli==1.1.0