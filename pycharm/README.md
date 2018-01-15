## What is this

A dockerfile which packs jetbrains pycharm into a container
so you can run it without installation on your system.

## Gotchas

If you get an error that it cannot connect to your display you need to set your xhost options so it has permission to connect.

## Docker run Example

docker run -it \
	--net host \
	--cpuset-cpus 0 \
	--memory 1500mb \
	-v /tmp/.X11-unix:/tmp/.X11-unix \
	-e DISPLAY=unix$DISPLAY \
	-e GOPATH=/projects/project1
	--security-opt seccomp=$HOME/goland.json \
	--device /dev/snd \
	--device /dev/dri \
	-v /dev/shm:/dev/shm \
	-v $HOME/.pycharm:/home/pycharm \
	--name pycharm \
	--rm \
	krystan/pycharm

## Motivation

I wanted a container that had my favourite python IDE in it so I did not need to install the software on my system each time.

## Installation

docker build -t <yourtag> .

## License

A short snippet describing the license (MIT, Apache, etc.)
