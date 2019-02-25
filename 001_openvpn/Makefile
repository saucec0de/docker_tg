EASY_RSA=EasyRSA-3.0.4

all:
	docker build -t tg_vpn .

ca:
	tar xvzf $(EASY_RSA).tgz
	cp Makefile $(EASY_RSA)
	cd $(EASY_RSA); make ca_step2

ca_step2:
	#@echo "STEP 2"
	#@cp vars.example vars
	#@# remove lines which match pattern
	#@sed -i '/EASYRSA_REQ_COUNTRY/d' vars
	#@sed -i '/EASYRSA_REQ_PROVINCE/d' vars
	#@sed -i '/EASYRSA_REQ_CITY/d' vars
	#@sed -i '/EASYRSA_REQ_ORG/d' vars
	#@sed -i '/EASYRSA_REQ_EMAIL/d' vars
	#@sed -i '/EASYRSA_REQ_OU/d' vars
	#@echo 'set_var EASYRSA_REQ_COUNTRY    "DE"'                       >> vars
	#@echo 'set_var EASYRSA_REQ_PROVINCE   "Bavaria"'                  >> vars
	#@echo 'set_var EASYRSA_REQ_CITY       "Munich"'                   >> vars
	#@echo 'set_var EASYRSA_REQ_ORG        "Siemens CT"'               >> vars
	#@echo 'set_var EASYRSA_REQ_EMAIL      "tiago.gasiba@siemens.com"' >> vars
	#@echo 'set_var EASYRSA_REQ_OU         "Security Lifecycle"'       >> vars
	## ######## SERVER #######
	#@./easyrsa init-pki
	#@echo "SEL-CA" | ./easyrsa build-ca nopass
	#@echo "server" | ./easyrsa gen-req server nopass
	##@./easyrsa import-req pki/reqs/server.req server
	#@echo "yes" | ./easyrsa sign-req server server
	#@./easyrsa gen-dh
	#@/usr/sbin/openvpn --genkey --secret ta.key
	## ######## CLIENT #######
	#@echo "client1" | ./easyrsa gen-req client1 nopass
	#@echo "yes" | ./easyrsa sign-req client client1
	@rm -rf ../client.ovpn
	@cp ../client.ovpn.tpl ../client.ovpn
	@echo "<key>"                             >> ../client.ovpn
	@cat pki/private/client1.key              >> ../client.ovpn
	@echo "</key>"                            >> ../client.ovpn
	@echo "<cert>"                            >> ../client.ovpn
	@openssl x509 -in pki/issued/client1.crt  >> ../client.ovpn
	@echo "</cert>"                           >> ../client.ovpn
	@echo "<ca>"                              >> ../client.ovpn
	@cat pki/ca.crt                           >> ../client.ovpn
	@echo "</ca>"                             >> ../client.ovpn
	@echo "key-direction 1"                   >> ../client.ovpn
	@echo "<tls-auth>"                        >> ../client.ovpn
	@cat ta.key                               >> ../client.ovpn
	@echo "</tls-auth>"                       >> ../client.ovpn

shell:
	docker run -p 1194:1194/udp --cap-add=NET_ADMIN -it tg_vpn /bin/bash

clean:
	rm -rf $(EASY_RSA)
