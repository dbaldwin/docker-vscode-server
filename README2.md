# Build the base image

docker build --build-arg USER=${USER} --build-arg UID=${UID} --build-arg=GID=${GID} -f versions\Dockerfile.base -t vscode:base .

# Build the python image

docker build --build-arg USER=${USER} --build-arg UID=${UID} --build-arg=GID=${GID} -f versions\Dockerfile.python -t vscode:python .

# Run the python image

docker run -it --rm -e PASSWORD=password -e DOCKER_USER=${USER} -p 8080:8080 -v $PWD/workspace:/home/coder/workspace -v $PWD/config:/home/coder/.config vscode:python
