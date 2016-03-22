# Change Pineapple Web UI to SSL

## Why

As the WiFi Pineappple has become more popular, it has also become more of a target. By default, the WebUI is served using HTTP which is unencrypted. This means that anyone also connected to the Pineapple over WiFi could sniff the network traffic and possibly be able to determine the authentication details to be able to access the WebUI themselves. A solution to this is to use SSL encryption over the HTTP connection (otherwise known as HTTPS).

## Install Packages
There are a few packages that we will need to install first.

Note: You will need an active internet connection on your Pineapple to perform this step.

```
opkg update
opkg --dest usb install libopenssl
opkg --dest usb install openssl-util
```

## Create config files
Next we need to configure SSL.

```
mkdir -p /etc/ssl/certs
nano /etc/ssl/openssl.cnf
```

Here is an openssl.cnf if you don't want to customize anything:

```
dir					= .

[ ca ]
default_ca				= CA_default

[ CA_default ]
serial					= $dir/serial
database				= $dir/certindex.txt
new_certs_dir				= $dir/certs
certificate				= $dir/cacert.pem
private_key				= $dir/private/cakey.pem
default_days				= 365
default_md				= md5
preserve				= no
email_in_dn				= no
nameopt					= default_ca
certopt					= default_ca
policy					= policy_match

[ policy_match ]
countryName				= match
stateOrProvinceName			= match
organizationName			= match
organizationalUnitName			= optional
commonName				= supplied
emailAddress				= optional

[ req ]
default_bits				= 2048			# Size of keys
default_keyfile				= key.pem		# name of generated keys
default_md				= md5				# message digest algorithm
string_mask				= nombstr		# permitted characters
distinguished_name			= req_distinguished_name
req_extensions				= v3_req

[ req_distinguished_name ]
# Variable name				Prompt string
#-------------------------	  ----------------------------------
0.organizationName			= Organization Name (company)
organizationalUnitName			= Organizational Unit Name (department, division)
emailAddress				= Email Address
emailAddress_max			= 40
localityName				= Locality Name (city, district)
stateOrProvinceName			= State or Province Name (full name)
countryName				= Country Name (2 letter code)
countryName_min				= 2
countryName_max				= 2
commonName				= Common Name (hostname, IP, or your name)
commonName_max				= 64

# Default values for the above, for consistency and less typing.
# Variable name				Value
#------------------------	  ------------------------------
0.organizationName_default		= Hak5
localityName_default			=
stateOrProvinceName_default		=
countryName_default			= UK
commonName				= pineapple

[ v3_ca ]
basicConstraints			= CA:TRUE
subjectKeyIdentifier			= hash
authorityKeyIdentifier			= keyid:always,issuer:always

[ v3_req ]
basicConstraints			= CA:FALSE
subjectKeyIdentifier			= hash
```

## Prepare Certificates
Now we begin creating our certificates which will be used in the encryption process.

```
cd /etc/ssl/certs
```

### Make Private Keys
To generate the private SSL keys, issue the following commands:

```
openssl genrsa -aes128 -out server.key 2048
openssl genrsa -aes128 -out ca.key 2048
```

### Remove Password From Private Key
We need to remove the password from our private key for obvious security reasons.

```
openssl rsa -in server.key -out server.key
```

### Generate CA Certificate
The CA certificate will be used to confirm the Pineapple's identity to our browser.

```
openssl req -new -x509 -days 3650 -key ca.key -out ca.pem
```

### Generate Certificate Signing Request
Using our CA certificate we "sign" our private key to confirm that the Pineapple is what we think it is.

```
openssl req -new -key server.key -out server.csr
```

### Self-Signed Certificate
Now we can self-sign our certificate.

```
openssl x509 -req -days 3650 -in server.csr -CA ca.pem -CAkey ca.key -set_serial 01 -out server.pem
```

Note: Don't forget to install the self-made CA certificate (ca.pem) into your browsers certificate store.

## Nginx Configuration
Finally we need to edit our Nginx (the web server that runs on the WiFi Pineapple) configuration file.

Enter `nano /etc/nginx/nginx.conf` into the terminal and make the following changes:

```
	server {
	        listen       1471 ssl;		# Port, make sure it is not in conflict with another http daemon.
	        server_name  pineapple;	# Change this, reference -> http://nginx.org/en/docs/http/server_names.html
                ssl_certificate     /etc/ssl/certs/server.pem;
                ssl_certificate_key /etc/ssl/certs/server.key;
                ssl_protocols       SSLv3 TLSv1 TLSv1.1 TLSv1.2;
                ssl_ciphers         HIGH:!aNULL:!MD5;
```

Note: Don't forget to change the certificate and certificate key to whatever you named them in the earlier steps.

Now you can restart Nginx with:

```
/etc/init.d/nginx restart
```

You should now be able to access your WiFi Pineapple at [https://172.16.42.1:1471](https://172.16.42.1:1471) and log in securely over HTTPS!