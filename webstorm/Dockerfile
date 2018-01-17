FROM node:8.9.4-stretch
LABEL maintainer "Krystan Honour <krystan@gmail.com>"

# docker run -it \
#	--net host \
#	--cpuset-cpus 0 \
#	--memory 1500mb \
#	-v /tmp/.X11-unix:/tmp/.X11-unix \
#	-e DISPLAY=unix$DISPLAY \
#	--security-opt seccomp=$HOME/webstorm.json \
#	--device /dev/snd \
#	--device /dev/dri \
#	-v /dev/shm:/dev/shm \
#	-v $HOME/.webstormhome:/home/webstorm \
#	--name webstorm \
#	--rm \
#	krystan/webstorm

# Install webstorm

 WORKDIR /opt/webstorm

 ARG WEBSTORMVERSION=WebStorm-2017.3.3
 
 ENV DISPLAY=unix$DISPLAY

 RUN apt-get update && apt-get install -y \
	apt-transport-https \
	ca-certificates \
	libcanberra-gtk-module \
	curl \
	git-core \
	libsecret-1-0 gnome-keyring \
	gnupg \
	hicolor-icon-theme \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
	libpango1.0-0 \
	libpulse0 \
	libv4l-0 \
	fonts-symbola \
	--no-install-recommends 

RUN apt-get install -y python python3-software-properties

RUN curl -sSL -O https://download.jetbrains.com/webstorm/${WEBSTORMVERSION}.tar.gz \
	&& mkdir webstorm \
	&& tar -xzvf ${WEBSTORMVERSION}.tar.gz -C ./webstorm/ \
		--strip-components=1 \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /src/*.deb

RUN groupadd -g 999 webstorm \
    && useradd -r -u 999 -g webstorm -G audio,video webstorm \
    && mkdir -p /home/webstorm \
    && chown -R webstorm:webstorm /home/webstorm \
    && chown -R webstorm:webstorm /opt/webstorm 

RUN npm install -g --unsafe-perm  @angular/cli create-react-app react-scripts react-cli react-native-cli react

# Run webstorm as non privileged user

USER webstorm

# Autorun webstorm
CMD [ "./webstorm/bin/webstorm.sh" ]
