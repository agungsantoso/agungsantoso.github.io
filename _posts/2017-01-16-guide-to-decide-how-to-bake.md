---
layout: post
title: Guide to Decide What to Bake into an AWS AMI and What to Provision Using cloud-init
---

I like to separate out machine provisioning from environment provisioning.
In general, I use the following as a guide:

Build Phase:

* Build a Base Machine Image with something like Packer, including all software required to run your application. Create an AMI out of this.
* Install the application(s) onto the Base Machine Image creating an Application Image. Tag and version this artifact. Do not embed environment specific stuff here like database connections etc. as this precludes you from easily reusing this AMI across different environment runtimes.
* Ensure all services are stopped

Release Phase:

* Spin up an environment consisting of the images and infra required, using something like CFN.
* Use Cloud-Init user-data to configure the application environment (database connections, log forwarders etc.) and then start the applications/services

This approach gives the greatest flexibility and cleanly separates out the various concerns of a continuous delivery pipeline.