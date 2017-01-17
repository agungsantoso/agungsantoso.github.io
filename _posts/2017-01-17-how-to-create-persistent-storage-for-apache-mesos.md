---
layout: post
title: How to Create Persistent Storage for Apache Mesos
---

Here are a few upcoming features in Mesos to improve support for stateful services, and corresponding current workarounds.

1. <b>Persistent volumes</b>: When launching a task, you can create a volume that exists outside of the task’s sandbox and will persist on the node even after the task dies/completes. When the task exits, its resources — including the persistent volume — can be offered back to the framework, so that the framework can launch the same task again, launch a recovery task, or launch a new task that consumes the previous task’s output as its input. Current workaround: Persist your state in some known location outside the sandbox, and have your tasks try to recover it manually. Maybe persist it in a distributed filesystem/database, so that it can be accessed from any node.

2. <b>Disk Isolation</b>: Enforce disk quota limits on sandboxes as well as persistent volumes. This ensures that your storage-heavy framework won’t be able to clog up the disk and prevent other tasks from running. Current workaround: Monitor disk usage out of band, and run periodic cleanup jobs.

3. <b>Dynamic Reservations</b>: Upon launching a task, you can reserve the resources your task uses (including persistent volumes) to guarantee that they are offered back to you upon task exit, instead of going to whichever framework is furthest below its fair share. Current workaround: Use the slave’s --resources flag to statically reserve resources for your framework upon slave startup.