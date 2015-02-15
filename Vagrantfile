Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "snowplow-javascript-tracker"
  config.ssh.forward_agent = true

  config.vm.provider :virtualbox do |vb|
    vb.name = Dir.pwd().split("/")[-1] + "-" + Time.now.to_f.to_i.to_s
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize [ "guestproperty", "set", :id, "--timesync-threshold", 10000 ]
    # node is not particularly memory hungry
    vb.memory = 1024
  end

  config.vm.provision :shell do |sh|
    sh.path = "vagrant/up.bash"
  end

  # Forward guest ports for Mountebank
  # Send traffic -> imposter
  config.vm.network "forwarded_port", guest: 4545, host: 4545
  # Query imposter
  config.vm.network "forwarded_port", guest: 2525, host: 2525

end
