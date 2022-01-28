FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

# systemctl
RUN apt update
RUN apt-get install -y systemctl

# curl
RUN apt update && apt -y upgrade
RUN apt install -y curl 

# git
#RUN apt install -y software-properties-common
#RUN apt update
#RUN add-apt-repository -y ppa:git-core/ppa
RUN apt install -y git
RUN git config --global init.defaultBranch main

# github cli
RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null
RUN apt update 
RUN apt install -y gh

# node.js 14
# https://computingforgeeks.com/install-node-js-14-on-ubuntu-debian-linux/
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt install -y nodejs

# ruby

# python
#RUN apt update
#RUN apt install -y software-properties-common
#RUN apt add-apt-repository ppa:deadsnakes/ppa
#RUN apt update
RUN apt-get install -y python3.9
RUN apt-get install -y python3-pip
RUN apt-get install -y libpq-dev

# postgresql
#RUN apt update
#RUN apt install -y postgresql postgresql-contrib
#RUN apt install -y wget curl ca-certificates 
#RUN apt install -y gnupg
#RUN wget -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - 
#RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ focal-pgdg main" >> /etc/apt/sources.list.d/pgdg.list' 
#RUN apt update
#RUN apt-get install postgresql postgresql-contrib 
#RUN apt-get install -y postgresql-client
#RUN apt-get install -y postgresql postgresql-contrib 
RUN apt -y install vim bash-completion wget
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" | tee  /etc/apt/sources.list.d/pgdg.list
RUN apt update
RUN apt install -y postgresql-13 postgresql-client-13

# redis
RUN apt update
RUN apt install -y redis-server
RUN cp -rp /etc/redis/redis.conf /etc/redis/redis.conf.bk
COPY redis.conf /etc/redis/redis.conf
#RUN redis-server /etc/redis/redis.conf

# heroku cli
RUN curl https://cli-assets.heroku.com/install.sh | sh

# run postgresql
RUN mkdir -p -m 777 /var/lib/postgresql/data && chown postgres:postgres /var/lib/postgresql/data
RUN mkdir -p -m 777 /run/postgresql && chown postgres:postgres /run/postgresql
RUN su postgres -c '/usr/lib/postgresql/13/bin/initdb -D /var/lib/postgresql/data/'
RUN cp -rp /var/lib/postgresql/data/pg_hba.conf /var/lib/postgresql/data/pg_hba.conf.bk
COPY pg_hba.conf /var/lib/postgresql/data/pg_hba.conf
#RUN su postgres -c '/usr/lib/postgresql/13/bin/pg_ctl start -D /var/lib/postgresql/data/'

# modify /root/.bashrc
RUN cp -rp /root/.bashrc /root/.bashrc.bk
RUN echo "redis-server /etc/redis/redis.conf" >> /root/.bashrc
RUN echo "su postgres -c '/usr/lib/postgresql/13/bin/pg_ctl start -D /var/lib/postgresql/data/'" >> /root/.bashrc