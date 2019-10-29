### VMware
---

- VMware Work Station Player 
- VMware Work Station Player Pro
https://my.vmware.com/jp/web/vmware/free#desktop_end_user_computing/vmware_workstation_player/15_0
https://my.vmware.com/en/web/vmware/free#desktop_end_user_computing/vmware_workstation_player/14_0

---
.rb vsphere
https://github.com/nsidc/vagrant-vsphere

.py workstation mac
https://github.com/DrDonk/unlocker

```rb
Vagrant.configure("2") do |config|
  config.vm.box = 'dummy'
  config.vm.box_url = './example_box/dummy.box'
  
  config.vm.provider :vsphere do |vsphere|
    vsphere.host = 'HOST NAME OF YOUR VSPHERE INSTANCE'
    vsphere.compute_resource_name = 'YOUR COMPUTE RESOURCE'
    vsphere.resource_pool_name = 'YOUR COMPUTE RESOURCE'
    vsphere.template_name = '/PATH/TO/YOUR VM TEMPLATE'
    vsphere.name = 'NEW VM NAME'
    vsphere.user = 'YOUR VMWARE USER'
    vsphere.password = 'YOUR VMWARE PASSWORD'
  end
end

vsphere.addressType = 'Manual'
vsphere.mac = '00:50:56:XX:YY:ZZ'

VAGRANT_INSTANCE_NAME = "vagrant-vsphere"

Vagrant.configure("2") do |config|
  config.vm.box = 'vsphere'
  config.vm.box_url = 'https://vagrantcloud.com/ssx/boxes/vsphere-dummy/versions/0.0.1/providers/vphere.box'
  
  config.vm.ostname = VAGRANT_INSTANCE_NAME
  config.vm.define VAGRANT_INSTANCE_NAME do |d|
  end
  
  config.vm.provider :vsphere do |vsphere|
    vsphere.host = 'vsphere.local'
    vsphere.name = VAGRANT_INSTANCE_NAME
    vsphere.compute_resource_name = 'vagrant01.vsphere.local'
    vsphere.resource_pool_name = 'vagrant'
    vsphere.template_name = 'vagrant-templates/ubuntu14041'
    vsphere.vm_base_path = "vagrant-machines"
    
    vsphere.user = 'vagrant-user@vsphere'
    vsphere.password = '***'
    vsphere.insecure = true
    
    vsphere.custom_attribute('timestamp', Time.now.to_s)
  end
end

```

```sh
vagrant plugin install vagrant-vsphere
tar cvzf dummy.box ./metadata.json
vagrant up --provider=vsphere
vagrant ssh
vagrant destroy
```

