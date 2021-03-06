# Easy Configuration of MacOS VMs using Puppet Bolt
A bolt project that configures MacOS machines with some packages via Homebrew. This is the initial version and it will go through further modifications as necessary.

# Setup
## Install VirtualBox, Vagrant and Bolt on your Laptop
### Virtualbox Install
* Install the latest virtualbox (v6.x) from https://www.virtualbox.org/
* Install the _VirtualBox 6.1.16 Oracle VM VirtualBox Extension Pack_ too. You might get prompted for it after the VirtualBox v6.x install. If not, download the Extension Pack and install it. Go to *File* -> *Preferences* -> *Extensions* Category.

### Vagrant Install 
Install Vagrant from https://www.vagrantup.com/downloads

### Install Puppet Bolt
Install Bolt from https://puppet.com/docs/bolt/latest/bolt_installing.html 

## Clone this Repository
* `git clone https://github.com/rajeshr264/macos-configuration-bolt.git` 
* `cd macos-configuration-bolt`

## Create 2 MacOSX Catalina VMs
The _Vagrantfile_ in the repository creates a Base MacOSX-Catalina VM and then 2 _linked clones_. In Virtualbox, you will see 3 VMs, namely the Base-VM and the 2 cloned VMs, called _mac1_ and _mac2_. The Base VM will be _powered off_ mode. We will be working with the _mac1_ and _mac2_ VMs only.

### Start the 2 VMs

To launch the downloading of the MacOSX Catalina Base Box & creation of the VMs, type:
* `vagrant up --provider virtualbox`

When you run the above command for the _first_ time, it will take a good *15-20 minutes* to download the MacOS X Catalina Base-Vagrant-box and then launch the 3 VMs. Go get a coffee. From then on, future `vagrant up` commands will launch the 2 VMs much faster.

To test if the VMs are up, open _VirtualBox_ GUI from your Desktop. You will see the Base-VM powered off and then 2 VMs running.

You can log into the 2 VMs that are running using the following ways:
* `ssh vagrant@mac1 or ssh vagrant@mac2` -> password: "vagrant"
* `cd macos-configuration-bolt` then `vagrant ssh mac1` or `vagrant ssh mac2`. vagrant will get the password specified in the _Vagrantfile_  

### Configure the 2 VMs using Bolt
In the _inventory.yaml_ file, you will see 2 VMs/nodes being listed there. Those 2 Private IPs are created and assigned in the _Vagrantfile_. 

Run the bolt command to configure the 2 VMs using a _sample_ script:
* `bolt script run scripts/setup_mac_sw.sh -t nodes`

The `nodes` target in the above bolt command, is defined in the _inventory.yaml_ file. 

This command will take 10 mins to run and you will not see any scrolling output. Just wait. You will see the entire output at the end.

After the command has finished, run the following command to check:

* `bolt command run 'java -version' -t nodes` to see if java 1.8 has been installed on both nodes.

# Cleanup
* `cd macos-configuration-bolt`
* `vagrant destroy -f`

The Base-VM will _not_ be deleted by the `vagrant destroy` command. I would recommend you leave it as a stopped VM. If/when you are done all your Mac related testing, you can delete the Base VM from Virtualbox UI.







