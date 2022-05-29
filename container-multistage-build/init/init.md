# Multistage builds

One of the most challenging things about building images is keeping the image size down. Each instruction in the Dockerfile/Containerfile adds a layer to the image, and you need to remember to clean up any artifacts you don’t need before moving on to the next layer. To write a really efficient Dockerfile/Containerfile, you have traditionally needed to employ shell tricks and other logic to keep the layers as small as possible and to ensure that each layer has the artifacts it needs from the previous layer and nothing else.

see: https://docs.docker.com/develop/develop-images/multistage-build/


