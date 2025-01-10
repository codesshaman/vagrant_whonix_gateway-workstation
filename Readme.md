# Vagrant virual machine with clean centos-8

Your need install vagrant and virtualbox for up this configuration.

Your need install [vagrant](https://github.com/hashicorp/vagrant-installers/releases/tag/v2.3.4.dev%2Bmain "vagrant") and  [virtualbox](https://www.virtualbox.org/ "virtualbox") for up this configuration. Optional you can use [make](https://www.gnu.org/software/make/ "make").

### Step 1

Download box ephillips/whonix-gateway for virtualbox from [vagrantup](https://portal.cloud.hashicorp.com/vagrant/discover/ephillips/whonix-gateway "vagrantup").

Download box ephillips/whonix-workstation for virtualbox from [vagrantup](https://portal.cloud.hashicorp.com/vagrant/discover/ephillips/whonix-workstation "vagrantup").

### Step 2

Clone this repository: git clone https://github.com/codesshaman/vagrant_whonix_gateway-workstation.git

### Step 3

Copy boxes and go inside the repository folder:

``cp ~/Downloads/900d4de6-73f2-4aa6-8198-adc2cd17f3f9 path_to/vagrant_whonix_gateway-workstation/workstation``

``cp ~/Downloads/736ae69e-396a-41ea-a790-6b6e4b05a8ec path_to/vagrant_whonix_gateway-workstation/gateway``

``cd vagrant_whonix_gateway-workstation``

### Step 4

Inicialize configuration:

``vagrant box add ephillips/whonix-gateway gateway``

``vagrant box add ephillips/whonix-workstation workstation``

or with make:

``make build``

### Step 5

Install configuration:

``vagrant up --provider=virtualbox``

or with make:

``make``

### Step 6

Connect:

``ssh vagrant@10.152.152.11``

or with make:

``make connect``
