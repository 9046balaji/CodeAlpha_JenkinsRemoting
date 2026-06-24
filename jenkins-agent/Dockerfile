# Official Jenkins SSH Agent base image
FROM jenkins/ssh-agent:jdk17

# Switch to root to install build tools
USER root

# Install Java build tools on the Agent
RUN apt-get update && apt-get install -y \
    curl \
    git \
    unzip \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Install Gradle 8.5 manually on the agent
ENV GRADLE_VERSION=8.5
ENV GRADLE_HOME=/opt/gradle/gradle-${GRADLE_VERSION}
ENV PATH=${GRADLE_HOME}/bin:${PATH}

RUN wget -q https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip \
    -O /tmp/gradle.zip && \
    mkdir -p /opt/gradle && \
    unzip -q /tmp/gradle.zip -d /opt/gradle && \
    rm /tmp/gradle.zip && \
    gradle --version

# Create a dedicated workspace directory for builds
RUN mkdir -p /home/jenkins/workspace && \
    chown -R jenkins:jenkins /home/jenkins/workspace

# Switch back to jenkins user
USER jenkins

# Verify Java and Gradle are available
RUN java -version && gradle --version
