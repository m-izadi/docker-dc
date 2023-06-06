# Run by CI/CD | Docker - Python
FROM python:3.10.8-slim-buster
MAINTAINER MohammadReza Izadi <mohammadreza.i1997@gmail.com>
ENTRYPOINT ["/bin/project"]
WORKDIR /opt
# COPY Dockerfile-build .

RUN apt update
##################################### Install Docker #####################################
RUN apt-get install -y ca-certificates curl gnupg lsb-release 
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
RUN apt update 2>/dev/null
RUN apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
##########################################################################################
RUN apt-get update && apt-get install -y \
  bzr \
  cvs \
  git \
  mercurial \
  subversion \
  && rm -rf /var/lib/apt/lists/*
##########################
RUN \
  git clone https://github.com/ATLANTBH/jmeter-components.git && \
  cd jmeter-components && \
  mvn clean install
###################################################
COPY requirements.txt /tmp/
RUN pip install --requirement /tmp/requirements.txt
COPY . /tmp/
##########################################################################################
COPY start.sh start.sh
CMD ["/start.sh"]
###################
VOLUME ["/root/.jenkins"]
##############
ADD http://wordpress.org/latest.tar.gz wordpress.tar.gz
CMD ["node", "src/index.js"]

EXPOSE 3000