# Change Pineapple Web UI to SSL

## Why

Since the Pineapples are prone to attacks, individuals love to sniff the clear-text credentials as you log into the HTTP interface. This quick guide should walk-through users' on how to protect themselves via SSL...

## Install Packages

```
opkg update
opkg --dest usb install libopenssl
opkg --dest usb install openssl-util
```

## Create config files

```
mkdir -p /etc/ssl/certs
nano /etc/ssl/openssl.cnf
```

example contents openssl.cnf:

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

```
cd /etc/ssl/certs
```

### Make Private Keys

```
openssl genrsa -aes128 -out server.key 2048
openssl genrsa -aes128 -out ca.key 2048
```

### Remove Password From Private Key

```
openssl rsa -in server.key -out server.key
```

### Generate CA Certificate

```
openssl req -new -x509 -days 3650 -key ca.key -out ca.pem
```

### Generate Certificate Signing Request

```
openssl req -new -key server.key -out server.csr
```

### Self-Signed Certificate

```
openssl x509 -req -days 3650 -in server.csr -CA ca.pem -CAkey ca.key -set_serial 01 -out server.pem
```

Note: Don't forget to install the self-made CA certificate (ca.pem) into your browsers certificate store.

## Nginx Configuration

Change `/etc/nginx/nginx.conf` to:

```
	server {
	        listen       1471 ssl;		# Port, make sure it is not in conflict with another http daemon.
	        server_name  pineapple;	# Change this, reference -> http://nginx.org/en/docs/http/server_names.html
                ssl_certificate     /etc/ssl/certs/server.pem;
                ssl_certificate_key /etc/ssl/certs/server.key;
                ssl_protocols       SSLv3 TLSv1 TLSv1.1 TLSv1.2;
                ssl_ciphers         HIGH:!aNULL:!MD5;
```

Note: don't forget to change the certificate and certificate key to as you've named them.

Then restart nginx

```
/etc/init.d/nginx restart
```