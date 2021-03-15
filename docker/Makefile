NAME=pogo
VERSION=9.7.3

default: image

build-files/.built: Dockerfile
	mkdir -p docker-build/pogo
	cp -r ../lib ../fr.esrf.tango.generator.xtend ../fr.esrf.tango.pogo ../fr.esrf.tango.pogo.parent ../fr.esrf.tango.pogo.ui ../org.tango.pogo.pogo_gui  docker-build/pogo/
	docker build --build-arg VERSION=$(VERSION) -t $(NAME):latest .
	touch docker-build/.built

lint:
	docker run --rm -i hadolint/hadolint < Dockerfile

image: build-files/.built

push: build-files/.built
	# User must set this environment variable if they want to push the image to a docker repo
	ifndef DOCKER_REGISTRY
		$(error DOCKER_REGISTRY is not set)
	endif

	docker tag ${NAME}:latest ${DOCKER_REGISTRY}/${NAME}
	docker push ${DOCKER_REGISTRY}/${NAME}

clean:
	rm -fr docker-build

.PHONY: default image clean
