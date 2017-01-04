---
layout: post
title: How to to run GoCD’s job and task with root permissions
---

First you need to be very careful since running commands as root is pretty dangerous. If you really have to do it, just add ‘go’ user to the group that can run ‘sudo’ and prefix all the commands that need root access with the ‘sudo’.
This is the case when you might want to use ‘shell-executor-task’ plugin https://github.com/gocd-contrib/script-executor-task rather than relying on built-in custom command executor. The reason to use shell-executor-task is that you can keep your privileged commands in the server config itself rather than in SCM so the access to the privileged commands will be limited to the server admin.
Also, instead of giving carte-blanche sudo access to the go user I’d further constraint the sudo privileges to only certain commands that really need it.
And last thing, I’d create a special task agent server that can run sudo commands and only let sudo jobs run on that agent. If this is to be done very infrequently so maintaining a task server is a waste of resources I would put this server in the VM or a docker container.
