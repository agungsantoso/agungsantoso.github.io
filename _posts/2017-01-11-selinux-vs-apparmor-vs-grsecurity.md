---
layout: post
title: SELinux vs AppArmor vs grsecurity 
---

I have done a lot of research in this area. I have even exploited AppArmor’s rulesets for MySQL. AppArmor is the weakest form of processes separation. The property that I’m exploiting is that all processes have write privileges to some of the same directories such as /tmp/. What nice about AppArmor is that it breaks some exploits without getting in the user/administrators way. However AppArmor has some fundamental flaws that aren't going to be fixed any time soon.

SELinux is very secure, its also very annoying. Unlike AppAmoror most legitimate applications will not run until SELinux has been reconfigured. Most often this results in the administrator misconfiguration SELinux or disabling it all together.

grsecurity is a very large package of tools. The one Ilike the most is grsecuirty’s enhanced chroot. This is even more secure then SELinux, although it takes some skill and some time to setup a chroot jail where as SELinux and AppAprmor “just work”.

There is a 4th system, a Virtual Machine. Vulnerabilities have been found in VM environments that can allow an attacker to “break out”. However a VM has a even greater separation than a chroot becuase in a VM you are sharing less resources between processes. The resources available to a VM are virtual, and can have little or no overlap between other VMs. This also relates to "cloud computing". In a cloud environment you could have a very clean separation between your database and web application, which is important for security. It also maybe possible that 1 exploit could own the entire cloud and all VM's running on it.