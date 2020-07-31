require_relative 'key_authorization'

Vagrant.configure('2') do |config|
  config.vm.box = "centos/7"
  authorize_key_for_root config, '/root/.ssh/id_dsa.pub', '/root/.ssh/id_rsa.pub'
  {
    'node1'    => '192.168.0.11',
    'node2'    => '192.168.0.12',
  }.each do |short_name, ip|
    config.vm.define short_name do |host|
      host.vm.network 'private_network', ip: ip
      host.vm.hostname = "#{short_name}"
    end

   #Playbook Ansible
   config.vm.provision "ansible" do |ansible|
      ansible.playbook = "/etc/ansible/playbooks/site.yml"
      ansible.config_file = "/etc/ansible/ansible.cfg"
   end
  end
end
