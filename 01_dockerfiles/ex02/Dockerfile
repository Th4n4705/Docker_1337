FROM ruby
RUN apt-get update && apt-get upgrade -y && apt-get install -y nodejs
ONBUILD COPY app /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD EXPOSE 3000
ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:seed 
#docker run -it --rm -p 3000:3000 ex02