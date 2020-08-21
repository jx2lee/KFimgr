# Kubeflow Image Loader Using Shell Script

This repo is for to pull/push docker image to private registry for Kubeflow.

## Usage

**Preperation**:  
Before Using Loader, Docker must be pre-installed. And Image capacity takes about 58G. Search Image list in `.imageList` and `.imageListHash` needed for Kubeflow installation *(version: 0.7.1)*  

**help**:  
Let's look at the script. For example:  
```bash
$ ./imageLoader
usage:
    ./imageLoader pull
    ./imageLoader push
```

### pull

Use the pull option to convert the image needed for kubeflow installation into a tar file. At this time, the tar file is created in `archive` folder and occupies about 58G. `.imageList` and` .imageListHash` contain lists with or without image tags(without image->hash).  

### push

This option pushes the image tar file in the `archive` folder to private docker registry. Before execution, the address must be added to `loader.config`. For example:  
```bash
#{ip}:{port}
#example) docker_registry=192.168.179.189:5000

docker_registry=
```

---

made by *jaejun.lee*
