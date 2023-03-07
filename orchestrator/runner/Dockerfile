FROM ubuntu:focal-20221130

ENV TZ=Europe/Paris
ENV DEBIAN_FRONTEND=noninteractive

COPY /apt-requirements.txt /tmp/apt-requirements.txt

RUN echo 'Acquire::http::Proxy "http://douziecr:etBAsgsK3%2Ad9.9dj3YP-Q.@proxy-http.esisar.grenoble-inp.fr:3128";' > /etc/apt/apt.conf.d/proxy.conf 
    && apt-get update
    && apt-get full-upgrade -y

# Copy ssh configuration file
COPY /root/ /
COPY /skel/ /home/otf

# Install OpenTestFactory & RobotFramework libraries as non-priviliged user
USER otf
RUN sudo ln -s /home/otf/.local/bin/robot /usr/bin/robot && \
    sudo mv /home/otf/environment /home/otf/.ssh

# Set PATH
ENV PATH="/home/otf/.local/bin:${PATH}"


WORKDIR /home/otf

# Enable SSH
EXPOSE 22
ENTRYPOINT bash /init.sh && bash /display.sh && sudo /etc/init.d/ssh restart && sudo service ssh restart