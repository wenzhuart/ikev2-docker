## IKEv2 Docker
forked from https://github.com/christophschlosser/ikev2-docker


#### Prerequisites

Install docker on your system and open port 500 and 4500 for UDP traffic in your firewall.


#### Build

	docker build -t ikev2_test .

#### Run for generate config

	docker run --rm --name=vpn-config -it -v $PWD/config:/config ikev2_test configure

#### Run server
	
	docker run --rm -d --privileged \
		--name=vpn-ikev2 \
		-v $PWD/config:/config \
		-p 500:500/udp -p 4500:4500/udp ikev2_test


- - -
Note:


certificate is stored in `$PWD/config/vpn-certs/`
