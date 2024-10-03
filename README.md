# ProxBox

## Run ProxMox in VirtualBox.

With a large Intel Mac, you can experiment with the ProxMox hypervisor.

- `brew bundle` will install python3
- Install Vagrant & VirtualBox with:
```
brew tap hashicorp/tap
brew install hashicorp/tap/hashicorp-vagrant
brew install --cask virtualbox
```
- `source install.rc` will install Ansible
- `vagrant up` will run ProxMox.
