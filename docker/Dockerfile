FROM openjdk
MAINTAINER Mike Wright "mwright@pivotal.io"
RUN wget -O cf-cli.deb https://cli.run.pivotal.io/stable?release=debian64
RUN wget -O cf-autopilot https://github.com/contraband/autopilot/releases/download/0.0.2/autopilot-linux
RUN wget -O local https://github.com/cloudfoundry-incubator/cflocal/releases/download/v0.18.0/cflocal-0.18.0-linux
RUN wget -O kubectl https://storage.googleapis.com/kubernetes-release/release/v1.9.3/bin/linux/amd64/kubectl

RUN mv kubectl /usr/local/bin/.
RUN dpkg -i cf-cli.deb
RUN chmod 755 cf-autopilot
RUN chmod 755 local
RUN cf install-plugin -f cf-autopilot
RUN cf install-plugin -f local

RUN git clone https://github.com/jwilliams-pivotal/pcf-ers-demo.git
RUN cd ./pcf-ers-demo && ./mvnw -f ./pom.xml package -DskipTests=true
RUN rm -rf ./pcf-ers-demo

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g newman

RUN apt-get -y install python-pip
RUN pip install docker-cloud

WORKDIR /data
