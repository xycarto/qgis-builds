# Set up for QGIS 3.28

BASEIMAGE := xycarto/qgis-builds
IMAGE := $(BASEIMAGE):3.34-2024-01-04

qgis: Dockerfile
	xhost + && \
	docker run -it --rm \
	--user=$$(id -u):$$(id -g) \
	-v $(HOME):/home/$(USER) \
	-v /usr/share/fonts/:/usr/share/fonts/ \
	-v /tmp/.X11-unix:/tmp/.X11-unix  \
	-e DISPLAY=$$DISPLAY \
	--privileged \
	-e HOME=$$HOME \
	--network host \
	-d \
	$(IMAGE)

# may need this: socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"
qgis-mac: Dockerfile
	xhost + && \
	docker run -it --rm \
	-v $(HOME):/home/$(USER) \
	-v /tmp/.X11-unix:/tmp/.X11-unix  \
	-e DISPLAY=`ipconfig getifaddr en0`:0 \
	--network host \
	-d \
	$(IMAGE)

docker: Dockerfile
	docker build --tag $(BASEIMAGE) - < $<  && \
	docker tag $(BASEIMAGE) $(IMAGE) && \
	docker push $(IMAGE) && \
	touch .push

docker-local: Dockerfile
	docker build --tag $(BASEIMAGE) . && \
	docker tag $(BASEIMAGE) $(IMAGE)  

docker-pull:
	docker pull $(IMAGE)