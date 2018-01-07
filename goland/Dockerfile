FROM debian:sid
LABEL maintainer "Krystan Honour <krystan@gmail.com>"

# docker run -it \
#	--net host \ # may as well YOLO
#	--cpuset-cpus 0 \ # control the cpu
#	--memory 1500mb \ # max memory it can use
#	-v /tmp/.X11-unix:/tmp/.X11-unix \ # mount the X11 socket
#	-e DISPLAY=unix$DISPLAY \
#	--security-opt seccomp=$HOME/chrome.json \
#	--device /dev/snd \ # so we have sound
#   --device /dev/dri \
#	-v /dev/shm:/dev/shm \
#	--name goland \
#	krystan/goland


# Install goland

 WORKDIR /opt/goland

 RUN apt-get update && apt-get install -y \
	apt-transport-https \
	ca-certificates \
	curl \
	gnupg \
	hicolor-icon-theme \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
	libpango1.0-0 \
	libpulse0 \
	libv4l-0 \
	fonts-symbola \
	--no-install-recommends \
	&& curl -sSL -O https://download.jetbrains.com/go/goland-2017.3.tar.gz \
	&& mkdir goland \
    && tar -xzvf goland-2017.3.tar.gz -C ./goland/ \
        --strip-components=1 \
    && rm *.tar.gz \
	&& apt-get purge --auto-remove -y curl \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /src/*.deb

RUN groupadd -r goland && useradd -r -g goland -G audio,video goland \
    && mkdir -p /home/goland && chown -R goland:goland /home/goland

# Run GoLand as non privileged user
USER goland

# Autorun GoLand
ENTRYPOINT [ "./goland/bin/goland.sh" ]