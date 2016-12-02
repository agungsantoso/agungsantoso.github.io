---
layout: post
title: How to Commit Changes to Docker Container
---

Occasionaly we have a docker container already running. We have made some configuration changes, let's say have added some host info in /etc/hosts inside the container. How do We keep the changes saved, so that next time when We open an interactive shell to the container We don't have to do the same stuff again? 

We can commit the changes we made by:

Short Command reference:

```
docker commit <container id or name>  <repository name>/<your image name>:<tage aka version>
```

Example:

```
docker commit c3f279d17e0a  myrepo/myimage:version3
```

Then you can use docker images to view your new Image after commit.

To run a container from your new Image:

```
docker run -d myrepo/myimage:version3 <optional startup command>
```

Another way would be creating your own image via dockerfile.