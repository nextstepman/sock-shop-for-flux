# sock-shop-for-flux

This repo shows how to deploy the sock shop to k8s with flux and at the same time explores possibilities to use kustomize to have different content for different environments.

# First install flux

```
helm init -c
helm repo add weaveworks https://weaveworks.github.io/flux
helm fetch weaveworks/flux --version 0.10.2 --untar
helm template flux --set git.url=git@github.com:nextstepman/test-flux-repo.git --set git.branch=master --set git.path=dev --set additionalArgs="{--manifest-generation=true}" | kubectl apply -f -
```

In the last argument, if you are not me (not the owner of this repo), better create a fork of this repo, as you need to have write access to use flux, as flux won't work without it, even if you use flux in a way that would not incur any change. Therefore fork it and replace the git url in above command.

After that, grant flux access. First get the public key of your installation

```
fluxctl identity
```

Next add that public key to your repo as deploy key with write access.

# Thats it

Now flux should have installed the contained application. Happy fluxing.




