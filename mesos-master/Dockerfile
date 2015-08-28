FROM garland/mesosphere-docker-base-image

# Installing zookeeper.  Seems to be a dependancy to mesos
# Not going to start it on runtime though
RUN sudo apt-get -y install zookeeperd
RUN echo 1 | sudo dd of=/var/lib/zookeeper/myid

# Install mesos.
RUN sudo apt-get -y install mesos /etc/mesos-slave
RUN sudo mkdir -p /etc/mesos-master
RUN echo in_memory | sudo dd of=/etc/mesos-master/registry
RUN echo 'docker,mesos' | sudo tee /etc/mesos-slave/containerizers

#-v /var/run/docker.sock:/var/run/docker.sock
VOLUME /var/run/docker.sock
# /usr/bin/docker:/usr/bin/docker
VOLUME /usr/bin/docker

# Not exposing port b/c you have to run the master in bridge net mode
#EXPOSE 5050

ENTRYPOINT ["mesos-master"]
