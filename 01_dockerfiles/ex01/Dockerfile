FROM debian
RUN	apt-get update
RUN	apt-get upgrade -y
RUN apt-get install bzip2 -y
RUN	apt-get install tar -y
RUN	apt-get install curl -y
RUN	curl -o team.tar.bz2 https://files.teamspeak-services.com/releases/server/3.9.1/teamspeak3-server_linux_amd64-3.9.1.tar.bz2
RUN	tar xfv team.tar.bz2
WORKDIR teamspeak3-server_linux_amd64
EXPOSE 9987/UDP 10011 30033
ENTRYPOINT sh ts3server_minimal_runscript.sh
#docker run -it -p 30033:30033 -p 10011:10011 -p 9987:9987/UDP -e TS3SERVER_LICENSE=accept ex01