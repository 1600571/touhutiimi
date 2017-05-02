Source: http://terokarvinen.com/2012/puppetmaster-on-ubuntu-12-04

# Puppet Master ja Slave

	sudo hostnamectl set-hostname chengdu
	ping chengdu
	sudo service avahi-daemon restart
	ping chendu.local
	sudoedit /etc/hosts  <--- vaihta xubuntu nimi chengdu

**MASTER ONLY**
	
	sudo apt-get -y install puppetmaster
	sudo service puppetmaster start
	sudoedit /etc/puppet/puppet.conf

	[master] kohdassa
	dns_alt_names = chengdu.local

	sudo service puppetmaster stop
	sudo rm -rf /var/lib/puppet/ssl/
	sudo service puppetmaster start

**AGENT ONLY**
	
	sudo puppet agent --enable
	sudo puppet agent --test --debug --verbose

	sudoedit /etc/puppet/puppet.conf

	[agent]
	server = chengdu.local
	sudo puppet agent --test --debug --verbose

	sudo puppet agent -tdv

**MASTER ONLY**
	
	cd /etc/puppet/modules
	ls
	sudo mkdir hellopanda
	cd hellopanda
	ls
	sudo mkdir manifests
	cd manifests
	sudoedit init.pp

	class hellopanda {
		file {'/tmp/hellopands.txt':
			content => "hello panda!\n",
		}	
	}

	cd ..
	cd ..
	cd ..
	/etc/puppet ls  ---> manifests

	cd manifests
	sudo nano site.pp --> sen sisään laita tämä:

	class {"hellopanda":}
	
**AGENT ONLY**

	sudo puppet agent -tdv
	
Pitäisi ottaa yhteyden masteriin
**MASTER ONLY**

	sudo puppet cert list  <-- listaa yhteyden ottaneet koneet
	sudo puppet help cert <-- antaa ohjeet mitä tehdä 
	sudo puppet cert sign (koneen nimi) <-- antaa certificaten tietylle koneelle 
	sudo puppet cert list -all <-- listaa kaikki yhteyttä ottaneet ja certifikoidut
	
	# (MUISTA 2 kertaa sudo puppet agent -tdv) ensimmäisellä kerralla se lähettää sign pyynnön, toinen kerta yhdistää).
	# Muista myös sudo puppet agent --enable jos ei toimi ekalla kerralla.
