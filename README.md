# vagrant-caldera

Easy local [Caldera](https://github.com/mitre/caldera) server VM for breach & attack simulation, using [Vagrant](https://www.vagrantup.com/) to provision.

*this is currently an older version on Caldera while I migrate into a repo*

```
vagrant up
```

Caldera will be running on http://172.30.1.2:8888 and only available from the current host and between local VMs by default.

Initial credentials are: `red`:` admin`

Password can be changed in the VM at `/home/vagrant/caldera/conf/local.yaml` which will require a restart of the service:

```
vagrant ssh
ps aux | grep server.py
kill #PID from above
sudo python3 server.py &
```

