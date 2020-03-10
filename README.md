![](https://img.shields.io/badge/license-GPL%20v3.0-brightgreen.svg)
![Maintenance](https://img.shields.io/maintenance/yes/2020)
<p align="right">
<img alt="gepardec" width=100px src="https://www.gepardec.com/files/gepardec_logo_light_background@2000w.png">
</p>
<br>
<br>

# vagrant-okd

We love to run okd on our workstations, but everybody uses a different operating system (Linux / MacOS / Windows). To reduce the pain of various nuances in the operating systems we have put okd in a vm that can be provisioned via Vagrant. Putting okd in a vm gives us the added benefit of controlling the resources it can consume on our workstations.

### Preflight

You can run okd on your workstation once you have 

* [Vagrant](https://www.vagrantup.com/intro/getting-started/install.html)
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads) or hyper-v for Windows

installed and downloaded this git repo. 

### Quickstart

To bootstrap the okd vm simply run

```
vagrant up
```

**Hint:** Windows user working with hyper-v can either add the `--provider hyperv` option to use hyper-v as provider if virtualbox is installed as well or set hyper-v default in the usercontext by setting the user environment variable in powershell via `[Environment]::SetEnvironmentVariable("VAGRANT_DEFAULT_PROVIDER", "hyperv", "User")`. Further documentation can be found here: https://docs.microsoft.com/en-us/virtualization/community/team-blog/2017/20170706-vagrant-and-hyper-v-tips-and-tricks 

**Hint:** the vm is only reachable from your host. You should not allow outside access since okd is configured to allow anyuser / anypassword to login. This is a local playground and should not be allowed to be accessed via the network.

### Access OKD

Open https://192.168.0.5:8443/console in your browser from your local workstation to access the okd web console.
**Hint:** if you use hyper-v you need to check the ip of your VM manually. The IP of a hyper-v vm can not be set to a static ip.

### Users

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