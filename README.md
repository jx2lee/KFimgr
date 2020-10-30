# KFimgr

This repo is for to pull or push docker image to private registry for Kubeflow.

## Usage

**Preperation**:  
Before Using Loader, Docker must be pre-installed. And Image capacity takes about 58G. Search Image list in folder `v0.7.0` and `v0.7.1` required for installation. You set config file `kfigmr.config`, For example:  
```bash
# Set KF Version & docker private registry
# example)
# kf_version=0.7.1 (0.7.1, 0.7.2, 1.0.2)
# docker_registry=192.168.179.185:5000
kf_version={install_version}
docker_registry={your_private_docker_registry_to_put_images}
```  

**help**:  
Let's look at the script. For example:  
```bash
$ ./imageLoader
usage:
    ./imageLoader pull
    ./imageLoader push
```

### pull

Use the pull option to convert the image needed for kubeflow installation into a tar file. At this time, the tar file is created in `archive` folder and occupies about 58G. `.imageList` and` .imageListHash` contain lists with or without image tags*(without image->hash).*  

### push
Use the push option to put the image required for installation into your private docker registry.

---

made by *jaejun.lee*
