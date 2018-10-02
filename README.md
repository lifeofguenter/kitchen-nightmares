# kitchen-nightmares
My excurse into being a top Chef.

## Chef

* https://docs.chef.io/install_server.html
* https://www.chef.sh/docs/chef-workstation/getting-started/
* https://www.digitalocean.com/community/tutorials/how-to-set-up-a-chef-12-configuration-management-system-on-ubuntu-14-04-servers

### Chef-server

* current release: https://downloads.chef.io/chef-server/current#ubuntu
* generally follow instructions: https://docs.chef.io/install_server.html

```bash
$ sudo apt -y -q install htop iftop iotop curl ca-certificates unzip
$ curl -LO# https://packages.chef.io/files/current/chef-server/12.18.13/ubuntu/16.04/chef-server-core_12.18.13-1_amd64.deb
$ sudo dpkg -i chef-server-core_12.18.13-1_amd64.deb
$ sudo chef-server-ctl reconfigure
```

Setup proper hostname: https://docs.chef.io/config_rb_server.html#recommended-settings

```bash
$ curl https://bootstrap.pypa.io/get-pip.py | sudo python
$ sudo -H pip install awscli
(this whole thing can most prolly be avoided by doing `knife ssl fetch`: https://getchef.zendesk.com/hc/en-us/articles/204831396-How-to-make-ChefDK-tools-trust-untrusted-SSL-certificates)
```

#### Create User

(dots in username are not allowed)

```bash
$ sudo chef-server-ctl user-create 'foobar' 'Foo' 'Bar' 'foobar@yourcompany.com' 'ReallyStr0ngPassword!' --filename foo.bar.pem
```

Add user to existing org

```bash
$ sudo chef-server-ctl org-user-add --admin lab foobar
```

#### Create Org

```bash
$ sudo chef-server-ctl org-create lab 'Lab Rats' --association_user 'foobar' --filename lab-validator.pem
```

### Chef-node

#### Bootstrapping

```bash
$ knife bootstrap 192.168.56.98 -x bofh --sudo -N node-hostname
```

#### Running chef-client

```bash
$ sudo chef-client
```

#### Editing



### Chef-Cookbooks

#### Create cookbook

* https://docs.chef.io/resource.html

```bash
$ chef generate cookbook chef-cookbook-nginx -m chef@yourcompany.com
```

#### Upload cookbook

(from inside the cookbook directory)

```bash
$ knife cookbook upload "${PWD##*/}" -o ..
```
