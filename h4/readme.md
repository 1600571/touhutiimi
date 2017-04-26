Source: http://terokarvinen.com/2012/puppetmaster-on-ubuntu-12-04

# Puppet Master ja Slave

	sudo hostnamectl set-hostname chengdu
	ping chengdu
	sudo service avahi-daemon restart
	ping chendu.local


	sudo apt-get -y install puppetmaster
	sudo service puppetmaster start
	sudo ls /var/lib/puppet/ssl/certs/
	sudo openssl x509 -in
	sudoedit /etc/puppet/puppet.conf

	[master]
	dns_alt_names = chengdu.local

	sudo service puppetmaster stop
	sudo rm -rf /var/lib/puppet/ssl/
	sudo service puppetmaster start
	sudo openssl x509 -ni /var/lib/puppet/ssl/certs/nimi -text|grep chengdu

	sudo puppet agent --test --debug --verbose
	sudo puppet agent --enable
	sudo puppet agent --test --debug --verbose

	sudoedit /etc/puppet/puppet.conf

	[agent]
	server = chengdu.local
	sudo puppet agent --test --debug --verbose

	sudo puppet agent -tdv

	cd /etc/puppet/modules
	ls
	sudo mkdir hellopanda
	cd hellopanda
	ls
	sudo mkdir manifests
	cd manifests
	sudoedit init.pp

	class hellopanda {
		file {"/tmp/hellopands.txt":
			content => "hello panda!\n",
		}	
	}

	cd ..
	cd ..
	cd ..
	/etc/puppet ls  ---> manifests

	cd manifests
	sudo nano site.pp

	class {"hellopanda":}

	sudo puppet agent -tdv
	ls /tmp/hellopanda.txt
	cat /tmp/hellopanda.txt

	sudo puppet cert list
	sudo puppet help cert
	sudo puppet cert sign (koneen nimi)
	sudo puppet cert list -all
	
	# (MUISTA 2 kertaa sudo puppet agent -tdv) ensimmäisellä kerralla se lähettää sign pyynnön, toinen kerta yhdistää).
	# Muista myös sudo puppet agent --enable jos ei toimi ekalla kerralla.
