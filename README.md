![Build Status](https://img.shields.io/travis/com/gepardec/vagrant-okd?style=flat-square)
![gplv3](https://img.shields.io/badge/license-GPL%20v3.0-brightgreen.svg?style=flat-square)
![maintenance](https://img.shields.io/maintenance/yes/2020?style=flat-square)
<p align="right">
<img alt="gepardec" width=100px src="https://www.gepardec.com/files/gepardec_logo_light_background@2000w.png">
</p>
<br>
<br>

# vagrant-okd

We love to run okd on our workstations, but everybody uses a different operating system (Linux / MacOS / Windows). To reduce the pain of various nuances in the operating systems we have put okd in a vm that can be provisioned via Vagrant. Putting okd in a vm gives us the added benefit of controlling the resources it can consume on our workstations. 

Yes, we are aware of [minishift](https://github.com/minishift/minishift). At the time of writing hyper-v support for minishift appears to be not fully functional for okd version 3.11.

## Preflight

You can run okd on your workstation once you have 

* [Vagrant](https://www.vagrantup.com/intro/getting-started/install.html)
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads) or hyper-v for Windows
* a good internet connection

and downloaded this git repo [gepardec/vagrant-okd](https://github.com/Gepardec/vagrant-okd/archive/master.zip). 

## Quickstart using virtualbox

To bootstrap the okd vm via virtualbox run

```
vagrant up
```

**Hint:** the vm is only reachable from your host. You should not allow outside access since okd is configured to allow anyuser / anypassword to login. This is a local playground and should not be allowed to be accessed via the network.

Next go to the **Access OKD** section to get information on how to access your okd instance.

---

## Quickstart using hyper-v

Why would you want to do that?! Well, if your system has hyper-v enabled, you can not run virtualbox since virtualbox requires hyper-v disabled to work. On the other hand you might like to run docker on your workstation too. Docker on windows requires hyper-v enabled. Hence a hyper-v supported setup is relevant.

To bootstrap the okd vm via hyper-v run

```
vagrant up --provider hyperv
```

Please take note of the ip assigned to your VM. You will need it in the next step. You can find the assigned ip in the output from your `vagrant up` command.

**Hint:** Windows user working with hyper-v can either add the `--provider hyperv` option to use hyper-v as provider if virtualbox is installed as well or set hyper-v as default in the usercontext by setting the user environment variable in powershell via `[Environment]::SetEnvironmentVariable("VAGRANT_DEFAULT_PROVIDER", "hyperv", "User")`. Further documentation can be found here: https://docs.microsoft.com/en-us/virtualization/community/team-blog/2017/20170706-vagrant-and-hyper-v-tips-and-tricks 

**Hint:** the vm is only reachable from your host. You should not allow outside access since okd is configured to allow anyuser / anypassword to login. This is a local playground and should not be allowed to be accessed via the network.

Once your vagrant box is provisioned we need to configure a bit of port forwarding.
Please execute the following command from a terminal (e.g. git bash, not powershell) within the git directory containing the Vagrantfile.

```
ssh vagrant@[YOUR_VM_IP_HERE] -i .vagrant/machines/default/hyperv/private_key -L 8443:127.0.0.1:8443 -L 80:127.0.0.1:80 -L 443:127.0.0.1:443
```

**Hint:** DO NOT CLOSE THE TERMINAL or you will loose your portforwardings!

Next go to the **Access OKD** section to get information on how to access your okd instance.

---

## Access OKD

### For virtualbox workstations
Open https://192.168.0.5:8443/console in your browser from your local workstation to access the okd web console.

### For hyper-v workstations
Open https://127.0.0.1:8443/console in your browser from your local workstation to access the okd web console.

**Hint:** if you use hyper-v you need to check the ip of your VM manually. The IP of a hyper-v vm can not be set to a static ip.

## Users

* **developer:** default user priveleges (any username / any password)
* **admin:** any password

---

## Customize the vm specs

You can alter the default configuration for the vagrant vm in the top section of the Vagrantfile

```ruby
#########################
$CPU = 2
$MEMORY = 4096
$CPUEXECUTIONCAP = 50 # does not work with hyper-v
$IP = "192.168.0.5"   # does not work with hyper-v # https://www.vagrantup.com/docs/hyperv/limitations.html
$BASEOS = "centos/7"
$SSH=2225
#########################
```


<!-- https://stackoverflow.com/questions/31828555/using-vagrant-on-cloud-ci-services/60380518#60380518 -->