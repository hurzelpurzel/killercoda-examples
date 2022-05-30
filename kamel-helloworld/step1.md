# Installing Kamel CLI tool

To start using Camel K you need the "kamel" CLI tool, that can be used to both configure the cluster and run integrations. Look into the link:https://github.com/apache/camel-k/releases for the latest version of the camel-k-client tool for your specific platform.

Download and uncompress the archive. It contains a small binary file named kamel that you should put into your system path. For example, if you are using Linux, you can put kamel in /usr/bin.

```
wget https://github.com/apache/camel-k/releases/download/v1.9.2/camel-k-client-1.9.2-linux-64bit.tar.gz
tar -xzf *.tar.gz
cp ./kamel /usr/bin
```{{exec}}


# Prerequisite: create a Image registry account
For this deme we need an external docker registry to push the Hello Word Image, if you don't have one, you can create a fre account for example at https://jfrog.com/container-registry


# Install the Operator

Create a secret with your registry username and password (please replace) :
```
kubectl -n default create secret docker-registry external-registry-secret --docker-username my-user --docker-password "password"
```{{copy}}

Install Camel K operator on the cluster in the default namespace:
```
kamel install --olm=false -n default --registry docker.io --organization my-org-or-username --registry-secret external-registry-secret --wait
```{{copy}}
Make sure to replace the my-org-or-username with your actual username or organization used to host the images.
