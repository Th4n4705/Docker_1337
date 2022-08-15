#FROM ubuntu
#RUN	apt-get update && apt-get upgrade -y
#RUN apt-get install curl -y
#RUN apt-get install bash -y
#RUN apt-get install openssh-server ca-certificates postfix -y
#RUN curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
#RUN sudo apt install gitlab-ce
#WORKDIR /etc/gitlab
#RUN echo "external_url 'http://192.168.99.100'"  > /etc/gitlab/gitlab.rb
#RUN sudo apt install letsencrypt -y
#RUN mkdir ssl
#WORKDIR SSL/
#RUN sudo openssl dhparam -out /etc/gitlab/ssl/dhparams.pem 2048
#RUN chmod 600 /etc/gitlab/ssl/*
#RUN echo "nginx['redirect_http_to_https'] = true" >> /etc/gitlab/gitlab.rb
#RUN echo nginx['ssl_certificate'] = "/etc/letsencrypt/live/gitlab.hakase-labs.co/fullchain.pem" >> /etc/gitlab/gitlab.rb
#RUN echo nginx['ssl_certificate_key'] = "/etc/letsencrypt/live/gitlab.hakase-labs.co/privkey.pem" >> /etc/gitlab/gitlab.rb
#RUN echo nginx['ssl_dhparam'] = "/etc/gitlab/ssl/dhparams.pem"  >> /etc/gitlab/gitlab.rb*/
FROM ubuntu
EXPOSE 443 80 22
RUN apt-get update && apt-get upgrade -y
RUN apt-get install ca-certificates openssh-server wget -y
RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh
RUN chmod 777 script.deb.sh
RUN ./script.deb.sh
RUN apt-get install gitlab-ce -y
RUN DEBIAN_FRONTEND=noninteractive apt install -y tzdata
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/ */tmp/* /var/tmp/*
WORKDIR /etc/gitlab
RUN echo "external_url 'https://10.11.9.14'" > gitlab.rb
RUN echo "nginx['enable'] = true" >> gitlab.rb
RUN echo "nginx['redirect_http_to_https'] = true" >> gitlab.rb
RUN echo "nginx['redirect_http_to_https_port'] = 80" >> gitlab.rb
RUN echo "letsencrypt['enable'] = false" >> gitlab.rb
RUN echo "nginx['ssl_certificate'] = \"/etc/gitlab/ssl/gitlab.crt\"" >> gitlab.rb
RUN echo "nginx['ssl_certificate_key'] = \"/etc/gitlab/ssl/gitlab.key\"" >> gitlab.rb
RUN echo "gitlab_rails['gitlab_shell_ssh_port'] = 22" >> gitlab.rb
RUN mkdir /etc/gitlab/ssl
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-subj "/C=MA/ST=0/L=Khourigba/O=rs1/OU=rs1/CN=10.11.9.14/emailAddress=t47waim@gmail.com" \
-keyout /etc/gitlab/ssl/gitlab.key -out /etc/gitlab/ssl/gitlab.crt
RUN export GIT_SSL_NO_VERIFY=1
RUN echo "service ssh start" > script.sh
RUN echo "(/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure && tail -f /dev/null" >> script.sh
RUN chmod 700 script.sh
ENTRYPOINT ./script.sh
#docker run -it -p 10.11.9.14:444:443 -p 10.11.9.14:80:80 -p 10.11.9.14:22:22 name
#git config --global http.sslVerify false
#docker run -it --privileged -p 80:80 -p 443:443 -p 2222:2222 {NAME}