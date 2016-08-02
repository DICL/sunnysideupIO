---
layout: post
title:  "Installing EclipseDFS locally"
date:   2016-07-31 17:00:00 +0200
categories: EclipseDFS install 
---

First of all, I would like to apologize the cumbersome installation process of EclipseDFS. The reason behind it is that we have a small team and our priorities at this moment is to add more features to our framework.

EclipseDFS audience are expected to be familiar with linux environments, thus we decided at this stage to let the [linux] user compile EclipseDFS, hoping that the user would add more features or fix bugs on his own. :)

*Currently, we are not distributing packages or binaries of EclipseDFS. The user is expected to download the latest 
version from our Github project site, and manually compile it and install it.*

# Step zero - Prerequisites 

Before you begin with this tutorial, there are some requirements in your cluster needed to run EclipseDFS.

Your cluster should have a partition shared in NFS among all the nodes. Also, most likely you will need
sudo permission on the master node unless you already have all the dependencies (you could also install them locally). 

If it is not your case you might have to tweek on your own some steps depending on your configuration.

# Dependencies

1. Relativitely new GCC (>=4.9) or clang (>=3.5) version.
2. Boost library version higher than 1.53.
3. Autotools.
4. Ruby interpreter >= 2.0.0 (For the launcher)

If you meet those requirements you can directly move to step one.

# Dependencies (only for UBUNTU)

*Ubuntu >= 14.04 is officially supported and its expected to work out of the box.*

We will begin by adding the repositories for the boost library and recent compiler versions:

{% highlight sh%}
$ sudo add-apt-repository ppa:ubuntu-toolchain-r-test
$ sudo add-apt-repository ppa:boost-latest
$ sudo apt-get update 
{% endhighlight %}

Next step will be installing the needed packages

{% highlight sh%}
$ sudo apt-get install libboost1.55-all-dev build-essential gcc-4.9 g++-4.9 
{% endhighlight %}

# Step one - Download and configuration

The step one begins downloading EclipseDFS from its github page:

{% highlight sh%}
$ git clone https://github.com/DICL/EclipseDFS.git
{% endhighlight %}

Then, we will create a temporary folder where we will hold all the intermediate files
needed for the compilation. This folder can be safely removed after installation.

{% highlight sh%}
$ mkdir build_dfs
{% endhighlight %}

The configuration script will be generated using the `autogen.sh` script shipped with EclipseDFS:

{% highlight sh%}
$ cd EclipseDFS
$ sh autogen.sh
{% endhighlight %}

Finally, we move to our temporary folder and call our generated configure script. The configure script 
has many different options to tweek the future installation. In this tutorial, I introduce the prefix option
which define where the binaries will be installed. __IMPORTANT__, if you want to install EclipseDFS for all
the users you would to set the prefix `--prefix /usr/local`

{% highlight sh%}
$ cd ../build_dfs
$ sh ../EclipseDFS/configure --prefix ~/sandbox  # Set the prefix, many other options are available
{% endhighlight %}

Note that the configure script will check if your system meets the requirements for compilation, thus 
errors are to be expected. 

# Step two - Compilation and Installation

**For those who might want to contribute to EclipseDFS they might find themself keep compiling and installing 
EclipseDFS whenever they modify the source code.**

The step two begins in our temporary folder `build_dfs`, once there we would issue a single command to 
compile and install EclipseDFS:

{% highlight sh%}
$ make -j8 install
{% endhighlight %}

Now all the binaries have been copied to `~/sandbox/bin`. Thus, we want to access those binaries at any moment. 
In order to do that we would need to add `~/sandbox/bin` to our path:

{% highlight sh%}
$ echo "export PATH=/home/vicente/sandbox/bin:$PATH" >> ~/.bashrc
{% endhighlight %}

*change vicente to your user*

# Step three - Configuration files

As for this local installation, the configuration file should be placed inside `~/.eclipse.json`. luckily we have
a template (example) inside the EclipseDFS/doc folder:

{% highlight sh%}
$ cp EclipseDFS/doc/eclipse.json ~/
{% endhighlight %}

The documentation of the configuration file is extensive and we keep adding new options, for up-to-date 
documentation refer to this [reference] [json_ref].

# Step four - EclipseDFS default launcher 

EclipseDFS is not shipped with a launcher, the main reason is that we do not want to limit its usage to a single launcher.
For our future work we expect to support docker and other vm images along init.d and systemd scripts.

However, we have developed an small and useful launcher called `eclipsed`, which lets you launch, stop, and debug your 
EclipseDFS deployment. It is a ruby gem, thus the installation is as simple as:

{% highlight sh%}
$ gem install eclipsed
{% endhighlight %}

Finally, you can launch EclipseDFS:

{% highlight sh%}
$ eclipsed restart 
{% endhighlight %}

Check if all the instances are up, by:

{% highlight sh%}
$ eclipsed status 
{% endhighlight %}

If that is the case, congratulations!! you have installed EclipseDFS.

# Conclusion

EclipseDFS deployment is cumbersome, our team acknowledge that problem, so we are looking forward ways to 
easy the deployment. Possibly you might have got stuck in some step, if that is the case you have few ways 
to get support from us (*From fastest to slowest*).

1. Reach us in our [slack room] [slack].
2. Submit a ticket in our [github site] [EclipseDFS_s].
3. E-mail any of our team (author list is in the README)


[EclipseDFS_s]: https://github.com/DICL/EclipseDFS/issues
[slack]:        https://dicl.slack.com/messages/general/
[json_ref]:     https://github.com/DICL/EclipseDFS/wiki/Configuration-file-reference
