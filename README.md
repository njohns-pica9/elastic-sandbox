Elastic Sandbox
==========

The purpose of this vagrant repository is to provide you with a simple elastic virtualmachine.

You will need a couple things, so continue reading.

## Requirements
  * [Vagrant](http://vagrantup.com) >= version 1.5.0
  * [Virtualbox](http://virtualbox.org) >= 4.3.0

## Usage
  * Install dependencies above
  * Install vagrant-omnibus via `vagrant plugin install vagrant-omnibus`
  * (Optional) install vagrant-vbguest via `vagrant plugin install vagrant-vbguest`
  * Clone this repository `git clone https:something elastic-sandbox`
  * Start the virtual machine and provisioning process via `cd elastic-sandbox && vagrant up`
  * Wait.. because installing java takes some time :)
  * Test it, (I'm using curl, you can use your browser as well): `curl http://localhost:9200?pretty`

## Learn
  * I am using the [official documentation](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/index.html) to learn more about [elasticsearch](http://www.elasticsearch.org), if there are other resources let me know.
  * I am using httpie, which is a nicer curl interface.. check it out here: [HTTPie](https://github.com/jkbr/httpie)
  * Sense was recently merged into Marvel, but you should be able to use it still.. checkout the elasticsearch documentation regarding Marvel.

## Known Issues
  1. I got some weird chef related errors, what do I do?
    * Timeouts suck.. try running `vagrant provision` or `vagrant reload --provision`
  2. Vagrant is having an issue mounting my directory (using virtualbox 4.3.10)
    *  See these links [Stackoverflow](http://stackoverflow.com/questions/22717428/vagrant-error-failed-to-mount-folders-in-linux-guest) and [Github](https://github.com/mitchellh/vagrant/issues/3341)
    * Then run `vagrant reload --provision`

## Contributing
Help me.