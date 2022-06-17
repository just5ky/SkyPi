<p align="center">
<img alt="SiYuan" src="https://b3log.org/images/brand/siyuan-128.png">
<br>
Build Your Eternal Digital Garden

![GitHub repo size](https://img.shields.io/github/repo-size/just5ky/siyuan?label=Repo%20Size&logo=github)
![Docker Pulls](https://img.shields.io/docker/pulls/justsky/siyuan)
![Docker Image Size (tag)](https://img.shields.io/docker/image-size/justsky/siyuan/master?color=blue&label=Container%20&logo=docker)

# [SiYuan](https://github.com/siyuan-note/siyuan)

## 💡 Introduction

SiYuan is a local-first personal knowledge management system, support fine-grained block-level reference and Markdown
WYSIWYG.

![feature0.png](https://b3logfile.com/file/2022/05/feature0-a82bdd3f.png)

![feature1-1.png](https://b3logfile.com/file/2022/05/feature1-1-740d9a02.png)


The easiest way to serve SiYuan on a server is to deploy it through Docker.

The overall program is located under /opt/siyuan/, which is basically the structure under the resources folder of the Electron installation package:

- appearance: icon, theme, multilingual
- guide: help documentation
- stage: interface and static resources
- kernel: kernel program

### Boot entry
The entry is set when building the Docker image: ENTRYPOINT [ "/opt/siyuan/kernel" ], use docker run justsky/siyuan with parameters to start:

--workspace specifies the workspace folder path, which is mounted to the container via -v on the host

For more parameters, please refer to --help. The following is an example of a startup command: 

```bash
docker run \
-v $DOCKERDIR/siyuan:/siyuan/workspace \
-p 6806:6806 \
-u 1000:1000 \
--restart: unless-stopped \
justsky/siyuan:master \ 
--workspace=/siyuan/workspace/
```

workspace_dir_host: The workspace folder path on the host
workspace_dir_container: The path of the workspace folder in the container, which is the same as specified by --workspace later

For simplicity, it is recommended to configure the workspace folder path to be the same on the host and container, for example, configure both workspace_dir_host and workspace_dir_container as /siyuan/workspace, and the corresponding startup command example: docker run -v /siyuan/workspace:/siyuan /workspace -p 6806:6806 -u 1000:1000 justsky/siyuan --workspace=/siyuan/workspace/

### User rights
In the image, the normal user siyuan (uid 1000/gid 1000) created by default is used to start the kernel process, so when the host creates a workspace folder, please set the user group to which the folder belongs: chown -R 1000:1000 / siyuan/workspace, you need to start the container with the parameter -u 1000:1000.

### Hidden port
Port 6806 can be hidden using NGINX reverse proxy, please note:

Configure WebSocket Reverse /ws