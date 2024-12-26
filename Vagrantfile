# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"
  config.vm.box_version = "202407.23.0"
  config.vm.network "private_network", ip: "192.168.126.44"
  # Shared folder
  config.vm.synced_folder "./", "/vagrant"
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt install -y sendmail
    sudo mkdir /var/log/nginx
    sudo cp /vagrant/access.log /var/log/nginx/
    sudo cp /vagrant/nginx_log_report.sh /opt/
    sudo chmod +x /opt/nginx_log_report.sh
    TEMP_CRON=$(mktemp)
    sudo crontab -l >> $TEMP_CRON
    echo "0 * * * * /opt/nginx_log_report.sh" >> $TEMP_CRON
    sudo crontab $TEMP_CRON
    rm $TEMP_CRON
    SHELL
end
