RELAYER_TAG := $(shell grep '^ENV RELAYER_TAG' cosmos-relayer/Dockerfile | cut -f3 -d\ )

all: babylond cosmos-relayer

babylond: babylond-rmi
	docker build --tag babylonchain/babylond -f babylond/Dockerfile \
    		$(shell git rev-parse --show-toplevel)

babylond-rmi:
	docker rmi babylonchain/babylond 2>/dev/null; true

cosmos-relayer: cosmos-relayer-rmi
	docker build --tag babylonchain/cosmos-relayer:${RELAYER_TAG} -f cosmos-relayer/Dockerfile \
				$(shell git rev-parse --show-toplevel)/contrib/images/cosmos-relayer
	docker tag babylonchain/cosmos-relayer:${RELAYER_TAG} babylonchain/cosmos-relayer:latest

cosmos-relayer-rmi:
	docker rmi babylonchain/cosmos-relayer 2>/dev/null; true

.PHONY: all babylond cosmos-relayer babylond-rmi cosmos-relayer-rmi
