#!/usr/bin/make -f

REGISTRY=srijanlabs/php-fpm-apache
#docker build --build-arg PHP_TAG=7.3-1.x -t srijanlabs/php-fpm-apache:7.3-1.x .
define build_image
	docker build  --build-arg PHP_TAG=${1} -t $(REGISTRY):${1} .
	docker build  --build-arg PHP_TAG=${1}-dev -t $(REGISTRY):${1}-dev .
endef

define push_image
	# Pushing production images.
	docker push $(REGISTRY):${1}
	docker push $(REGISTRY):${1}-dev 

endef

build:
	# $(call build_image,7.2-1.x)
	$(call build_image,7.3-1.x)
	# $(call build_image,7.4-1.x)

push:
	$(call push_image,7.2-1.x)
	$(call push_image,7.3-1.x)
	$(call push_image,7.4-1.x)

.PHONY: *
