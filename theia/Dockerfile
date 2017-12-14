FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y build-essential curl software-properties-common python-software-properties zlib1g-dev liblzma-dev libpq-dev tzdata
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-add-repository ppa:brightbox/ruby-ng
RUN apt-get update
RUN apt-get install -y nodejs yarn ruby2.4 ruby2.4-dev
ARG version=latest
RUN useradd -ms /bin/bash theia
USER theia
WORKDIR /home/theia
ADD $version.package.json ./package.json
RUN yarn
RUN npx theia build
EXPOSE 3000
ENV SHELL /bin/bash
ENV GEM_HOME /home/theia/.gem
ENV GEM_PATH /home/theia/.gem
RUN echo 'PATH=/home/theia/.gem/bin:$PATH' >> /home/theia/.bashrc
ENTRYPOINT [ "npx", "theia", "start", "/home/project", "--hostname=0.0.0.0" ]
