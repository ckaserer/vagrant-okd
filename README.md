![Maintenance](https://img.shields.io/maintenance/yes/2019)
![GitHub](https://img.shields.io/github/license/gepardec/vagrant-okd)
<p align="right">
<img alt="gepardec" width=100px src="https://github.com/Gepardec/vagrant-okd/raw/master/.images/gepardec.png">
</p>
<br>
<br>

# vagrant-okd

We love to run okd on our workstations, but everybody uses a different operating system (Linux / MacOS / Windows). To reduce the pain of various nuances in the operating systems we have put okd in a VM that can be provisioned via Vagrant. Putting okd in a VM gives us the added benefit that we can control the resource it consumes on our workstations.

### Preflight

You can run okd on your workstation once you have 

* [Vagrant](https://www.vagrantup.com/intro/getting-started/install.html)
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

installed and downloaded this git repo. 

### Quickstart

To bootstrap the okd VM simply run

```
vagrant up
```

**Hint:** the VM is only reachable from your host. You should not allow outside access since okd is configured to allow anyuser / anypassword to login. This is a local playground and should not be allowed to be accessed via the network.### Access OKD

Open https://192.168.0.2:8443/console in your browser from your local workstation to access the okd web console.

### Users

* **developer:** default user priveleges (any username / any password)
* **admin:** any password

---

## Customize the VM specs

You can alter the default configuration for the Vagrant VM in the top section of the Vagrantfile

```ruby
#########################
$CPU = 4
$MEMORY = 8192
$CPUEXECUTIONCAP = 50
$IP = "192.168.0.2"
$BASEOS = "centos/7"
$SSH=2223
#########################
```