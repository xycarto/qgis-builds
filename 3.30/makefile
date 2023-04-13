# Set up for QGIS 3.28

BASEIMAGE := xycarto/qgis-builds
IMAGE := $(BASEIMAGE):3.30-2023-04-14

qgis-docker: Dockerfile
	docker build --tag $(BASEIMAGE) . && \
	docker tag $(BASEIMAGE) $(IMAGE)  

qgis: Dockerfile
	xhost + && \
	docker run -it --rm \
	-v $(HOME):/home/$(USER) \
	-v /usr/share/fonts/:/usr/share/fonts/ \
	-v /tmp/.X11-unix:/tmp/.X11-unix  \
	-e DISPLAY=$$DISPLAY \
	--network host \
	-d \
	$(IMAGE)