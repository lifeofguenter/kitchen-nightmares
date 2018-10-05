# Knife

## Setup

* https://downloads.chef.io/chefdk/current#mac_os_x
* multiple knife configs: http://spuder.github.io/2015/knife-multiple-chef-server-orgs/

If using ed25519 ssh keys you need to additionally do this:

```bash
$ brew install libsodium
$ sudo chef gem install rbnacl -v 4.0.2
$ sudo chef gem install rbnacl-libsodium bcrypt_pbkdf

(alternatively try: sudo /opt/chefdk/embedded/bin/gem install)
```

Add private ssh-key to agent (not sure why I need to do this):

```bash
$ ssh-add ~/.ssh/id_ed25519
```

## Status

This command is quite useful to check when a node last run `chef-client`:

```bash
$ knife status 'name:ip-172-30-0-210*'
20 minutes ago, ip-172-30-0-210.eu-west-1.compute.internal, ubuntu 16.04.
```

(`QUERY` format: https://docs.chef.io/knife_search.html)
