# Official Jenkins LTS image
FROM jenkins/jenkins:lts-jdk17

# Skip the initial setup wizard (we configure programmatically)
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"

# Switch to root to install extra tools
USER root

# Install Docker CLI and other tools inside Controller
RUN apt-get update && apt-get install -y \
    curl \
    git \
    openssh-client \
    && rm -rf /var/lib/apt/lists/*

# Switch back to jenkins user for security
USER jenkins

# Pre-install required plugins using Jenkins Plugin CLI
RUN jenkins-plugin-cli --plugins \
    ssh-slaves \
    workflow-aggregator \
    git \
    gradle \
    pipeline-stage-view \
    blueocean \
    credentials-binding \
    ssh-credentials \
    antisamy-markup-formatter

# Set timezone
ENV TZ=Asia/Kolkata

EXPOSE 8080 50000
