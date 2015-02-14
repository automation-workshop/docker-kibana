# -*- mode: ruby -*-
# vi: set ft=ruby :
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'

Vagrant.configure(2) do |config|
  config.vm.provider "docker" do |d|
    d.vagrant_machine = "docker-host"
    d.vagrant_vagrantfile = "host/Vagrantfile"
  end

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define :elasticsearch do |cfg|
    cfg.vm.hostname = "elasticsearch"
    cfg.vm.provider "docker" do |d|
      d.name = cfg.vm.hostname
      d.image = "elasticsearch"
      d.ports = ["9200:9200", "9300:9300"]
      d.volumes = ["/esdata:/usr/share/elasticsearch/data"]
    end
  end

  config.vm.define :kibana do |cfg|
    cfg.vm.hostname = "kibana"
    cfg.vm.provider "docker" do |d|
      d.name = cfg.vm.hostname
      d.image = "marcbachmann/kibana4"
      d.ports = ["5601:5601"]
      d.env = {
        "ELASTICSEARCH" => "http://es:9200",
        "REQUEST_TIMEOUT" => "30000"
      }
      d.link "elasticsearch:es"
    end
  end

end
