# Definitions
build_output = runtime/kallisto_sc
runtime_fullpath = $(realpath runtime)
build_tool = runtime-container.DONE
git_commit ?= $(shell git log --pretty=oneline -n 1 -- ../kallisto_sc | cut -f1 -d " ")
name = quay.io/ucsc_cgl/kallisto_sc
# pachterlab commit: 0469873
tag = 0469873--${git_commit}

# Steps
docker:
	docker build -t ${name}:${tag} .
	-docker rmi ${name}:latest
	docker tag ${name}:${tag} ${name}:latest
	touch ${build_tool}

push: docker
	# Requires ~/.dockercfg
	docker push ${name}:${tag}
	docker push ${name}:latest

test: docker
	python test.py

clean:
	-rm ${build_tool}
	-rm ${build_output}
