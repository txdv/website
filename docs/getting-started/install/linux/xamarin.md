---
title: Newest Debian packages by Xamarin
redirect_from:
  - /DistroPackages/Xamarin/
---

Xamarin Packages
----------------

Xamarin ships its own debian packages under [http://download.mono-project.com](http://download.mono-project.com).
The following instructions will show you how to install the latest Xamarin mono packages on debian based distributions.

First of all we need to append the Xamarin package repository to /etc/apt/sources.list:

``` bash
deb http://download.mono-project.com/repo/debian wheezy main
```

This can be achieved by executing the following command as root:

``` bash
echo "deb http://download.mono-project.com/repo/debian wheezy main" > /etc/apt/sources.list.d/xamarin

```

In order for apt to verify the packages the public Xamarin key has to be added to the apt key list:

``` bash
curl http://download.mono-project.com/repo/xamarin.gpg | apt-key add -
```

If curl is not available, wget can be used also:

``` bash
wget http://download.mono-project.com/repo/xamarin.gpg
apt-key add xamarin.gpg
```

An update is needed to fetch the contents of the newly added Xamarin repository.

``` bash
apt-get update
```

In order to verify that apt will install 3.6.0 apt-cache can be used:


``` bash
apt-cache policy mono-runtime
```

Which should return:

```
mono-runtime:
  Installed: (none)
  Candidate: 3.6.0-0xamarin1
  Version table:
 *** 3.6.0-0xamarin1 0
        500 http://download.mono-project.com/repo/debian/ wheezy/main amd64 Packages
        100 /var/lib/dpkg/status
     3.2.8+dfsg-4ubuntu1 0
        500 http://de.archive.ubuntu.com/ubuntu/ trusty/main amd64 Packages
```

Note the Candidate, the Xamarin packages are all suffixed with *-0xamarin1*.

Now apt can be used in the usual way to install the latest Xamarin packages:

```
apt-get install mono-complete
```

Short script
------------

If you just want to get going immediately, just run this script with root rights:

``` bash
#!/bin/bash

wget http://download.mono-project.com/repo/xamarin.gpg
apt-key add xamarin.gpg
rm xamarin.gpg

apt-get update

apt-get install mono-complete
```
