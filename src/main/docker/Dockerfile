# Version 1.1.0

FROM dockeredcom/debian-stretch:latest

MAINTAINER Yves Vindevogel (yves.vindevogel@dockered.com)

ENV SHELL=/bin/bash

# Yves Vindevogel
# 2018-08-15
# The line below is to prevent the following warning when doing the gpg -a export
# Warning: apt-key output should not be parsed (stdout is not a terminal)
# Solution derived from: https://stackoverflow.com/questions/48162574/how-to-circumvent-apt-key-output-should-not-be-parsed

ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update --yes
RUN apt-get upgrade --yes

RUN apt-get install dirmngr gnupg2 curl --yes --no-install-recommends

# Yves Vindevogel
# 2018-08-15
# Used to install Oracle JDK 8/9 from Ubuntu
# The documentation is found on Debian 8, but also applicable to Debian 9 (stretch)
# https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-get-on-debian-8
# If you follow the guide from Digital Ocean, you will get an error on the apt-get update because the key is not trusted
# Adding the key below solves that problem (but you run into others with debconf)
# As it is not the purpose to install Java here, the problem with debconf is not solved here

RUN gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C2518248EEA14886
RUN gpg -a --export C2518248EEA14886 | apt-key add -

# Yves Vindevogel
# 2018-08-16
# Key used by nginx

RUN curl -fsSL http://nginx.org/keys/nginx_signing.key | apt-key add -

RUN apt-get update --yes

RUN apt-get autoremove --yes
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD [ "/bin/bash" ]
