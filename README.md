<p align="center">
<img src="https://github.com/GGianluppi/darkweb_website/assets/104764600/325ce775-80b5-4314-9c9f-49df5ed8bd54" width=50% height=50%>
</p>


<h1 align="center">Create your own Dark Web website</h1>

This repository was developed based on the content presented in the YouTube video by **NetworkChuck**, available at **[YouTube](https://www.youtube.com/watch?v=CurcakgurRE&t=1s)**.<br/>

This project consists of two main parts: the first part involves the use of OnionShare, while the second part utilizes Nginx and mkp224o.

# PART 1

OnionShare is a powerful tool for securely and anonymously sharing files over the Tor network. This README will guide you through the installation process on Windows and Linux.

## Windows Installation

1. Visit the OnionShare website at **https://onionshare.org/**.
2. Download the Windows installer from the website.
3. Run the installer and follow the instructions.
4. Once the installation is complete, you can launch OnionShare from your Windows system.


## Linux Installation
**1. Install snapd** </br>
If you're using a Linux distribution that supports snap packages, you can install OnionShare using snapd.

Open a terminal and run the following command to install snapd:

	sudo apt install snapd
	
	
**2. Install OnionShare** </br>
After installing snapd, you can easily install OnionShare with the following command:

	sudo snap install onionshare
	

**3. Linux CLI Commands** </br>
To use OnionShare via the command-line interface (CLI), run the following command to display the available CLI options and commands:

	onionshare.cli --help
</br>
 
<p align="center">
<img src="https://github.com/GGianluppi/darkweb_website/assets/104764600/90a3345e-88ca-4858-945b-e003ded492a9" width=160% height=160%>
</p>

# PART 2

Nginx is a popular and high-performance open-source web server and reverse proxy server software. For more information about Nginx, you can visit the official website at **[NGINX](https://nginx.org/en/)**. 

## Setup Website (nginx)
**1. Install Nginx**</br>
Install Nginx, a web server software:

	sudo apt install nginx

**2. Copy website files to Nginx directory**</br>
Copy the website files from the Dark Web Supreme project to the Nginx directory:

	sudo cp -r ~/darkweb/website /var/www/

**3. Edit Nginx default website**</br>
Open the Nginx default website configuration file for editing:

	sudo nano /etc/nginx/sites-available/default
	
**4. Change Website location**</br>
Inside the configuration file, find the root directive and change it to point to your Dark Web website:

	root /var/www/website
	
**5. Test Nginx Config**</br>
Test the Nginx configuration to ensure there are no syntax errors:

	sudo nginx -t
	
**6. Restart Nginx**</br>
If the test is successful, restart Nginx to apply the changes:

	sudo systemctl restart nginx
	

## Install ToR
**1. Install Pre-Requisites**</br>
Install the required pre-requisites for Tor:

	sudo apt install apt-transport-https

**2. Check Debian Version**</br>
Check your Debian version by running:

	cat /etc/debian_version
	
**3. Create a new Tor repository file**</br>
Create a new file for the Tor repository configuration:

	sudo nano /etc/apt/sources.list.d/tor.list

**4. Add Tor repository configuration**</br>
Add the following lines to the tor.list file, replacing <DISTRIBUTION> with your Debian version:
	
	deb [signed-by=/usr/share/keyrings/tor-archive-keyring.gpg] https://deb.torproject.org/torproject.org <DISTRIBUTION> main
	deb-src [signed-by=/usr/share/keyrings/tor-archive-keyring.gpg] https://deb.torproject.org/torproject.org <DISTRIBUTION> main
	
**5. Add the GPG Key**</br>
Add the GPG key for the Tor repository:

	sudo apt update
	sudo apt install tor deb.torproject.org-keyring
	
**6. Configure Tor**</br>
Open the Tor configuration file for editing:

	sudo nano /etc/tor/torrc

**7. Uncomment Tor configuration lines**</br>
Uncomment the following lines in the torrc file:

	#HiddenserviceDir /var/lib/tor/hidden_service
	#HiddenServicePort 80 127.0.0.1:80
	
**8. Restart Tor**</br>
Restart the Tor service to apply the configuration changes:

	sudo systemctl restart tor

**9. See your onion address**</br>
To view your newly created .onion address, use the following command:

	cat /var/lib/tor/hidden_service/hostname



## Create a Vanity Onion Address
A vanity onion address is a customized and human-readable .onion address on the Tor network. For this purpose, we will use the tool 'mkp224o' to generate vanity onion addresses. For more information, you can visit **[mkp224o](https://github.com/cathugger/mkp224o)**.


**1. Install mkp224o**</br>
Install the pre-requisites required for mkp224o:

	sudo apt install gcc libc6-dev libsodium-dev make autoconf

**2. Download Git Repo**</br>
Clone the mkp224o Git repository:

	git clone https://github.com/cathugger/mkp224o.git
	
**3. Change directories**</br>
Change to the mkp224o directory:

	cd mkp224o
	
**4. Build mkp224o**</br>
Build mkp224o using the following commands:

	./autogen.sh
	./configure
	make
	
**5. Generate your key**</br>
Generate your custom .onion address key. Replace <KEY> with your desired key:

	./mkp224o <KEY> -v -n 1 -d ~/onionkey -t 4

**6. Copy your new key to the hidden service directory**</br>
Copy your generated key to the Tor hidden service directory:

	sudo cp -r ~/onionkey/youraddressname/ /var/lib/tor/hidden_service
	
**7. Restart Tor**</br>
Finally, restart the Tor service to apply the changes:

	sudo systemctl restart tor







