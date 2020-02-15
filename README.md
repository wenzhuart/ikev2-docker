## IKEv2 Docker
forked from https://github.com/christophschlosser/ikev2-docker


#### Prerequisites

Install docker on your system and open port 500 and 4500 for UDP traffic in your firewall.

#### clone from GitHub

	git clone https://github.com/wenzhuart/ikev2-docker

#### go working directory
	
	cd ikev2_docker

#### Build

	docker build -t ikev2_test .

#### Run for generate config

	docker run --rm --name=vpn-config -it -v $PWD/config:/config ikev2_test configure

then copy print-out as client cert locally

**local command:**

	touch vpn.pem
	echo "
	<paste print-out content here>
	" > vpn.pem


#### Run server
	
	docker run --rm -d --privileged --name=vpn-ikev2 -v $PWD/config:/config -p 500:500/udp -p 4500:4500/udp ikev2_test

#### Run server - docker-compose.yml

	ikev2:
	  image: ikev2_test
	  privileged: true
	  ports:
	    - "500:500/udp"
	    - "4500:4500/udp"
	  volumes:
	    - "$PWD/config:/config"
	  restart: always


- - -
Note:


certificate is stored in `$PWD/config/vpn-certs/`
