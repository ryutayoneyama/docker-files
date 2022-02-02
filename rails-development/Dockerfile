#FROM ruby:2.7-slim-bullseye
FROM ruby:3.0.3-slim-bullseye

RUN apt update && apt upgrade -y

# install necessary libraries
RUN apt install -y ruby-dev build-essential zlib1g-dev

# install rails
RUN gem install rails --no-document

# install curl
RUN apt install -y curl

# install nodejs,npm,yarn
RUN curl -fsSL https://deb.nodesource.com/setup_current.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g yarn

# install postgresql
RUN apt install -y postgresql-13
RUn mkdir -p -m 777 /var/lib/postgresql/data && chown postgres:postgres /var/lib/postgresql/data
RUN su postgres -c '/usr/lib/postgresql/13/bin/initdb -D /var/lib/postgresql/data/'
#RUN su postgres -c '/usr/lib/postgresql/13/bin/pg_ctl start -D /var/lib/postgresql/data'
RUN apt install -y libpq-dev

# install git cli
RUN apt update && apt upgrade -y
RUN apt install -y git
RUN git config --global init.defaultBranch main

# heroku cli
#RUN curl https://cli-assets.heroku.com/install-ubuntu.sh | sh

# you can execute following commands to create a new rails project!
# rails new --database postgresql blog
# su postgres -c '/usr/lib/postgresql/13/bin/createuser -r -d -P blog'
#Enter password for new role: 
#Enter it again: 
# --- update config/database.yml ---
# bin/rake db:create BLOG_DATABASE_PASSWORD='ora-600RYibmcrm'
# bin/rails server
