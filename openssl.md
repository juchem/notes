# generate certs
- script to generate self-signed dev certificates unnatended: ```
CA_CERT_DEV_PASSWORD="1234"

echo 01 > serial
[ -e index.txt ] && truncate --size=0 index.txt || touch index.txt

cat > openssl.cnf <<EOF
dir = .

[ ca ]
default_ca = CA_default

[ CA_default ]
serial = \$dir/serial
database = \$dir/index.txt
new_certs_dir = \$dir
certificate = \$dir/ca.crt
private_key = \$dir/ca.key
default_days = 365
default_md = sha512
preserve = no
email_in_dn = no
nameopt = default_ca
certopt = default_ca
policy = policy_match

[ policy_match ]
countryName = match
stateOrProvinceName = match
organizationName = match
organizationalUnitName = optional
commonName = supplied
emailAddress = optional

[ req ]
default_bits = 4096 # Size of keys
default_keyfile = dev.key # name of generated keys
default_md = sha512 # message digest algorithm
string_mask = nombstr # permitted characters
distinguished_name = req_distinguished_name
req_extensions = v3_req

[ req_distinguished_name ]
# Variable name   Prompt string
#----------------------   ----------------------------------
0.organizationName = Organization Name (company)
organizationalUnitName = Organizational Unit Name (department, division)
emailAddress = Email Address
emailAddress_max = 40
localityName = Locality Name (city, district)
stateOrProvinceName = State or Province Name (full name)
countryName = Country Name (2 letter code)
countryName_min = 2
countryName_max = 2
commonName = Common Name (hostname, IP, or your name)
commonName_max = 64

# Default values for the above, for consistency and less typing.
# Variable name   Value
#------------------------------   ------------------------------
0.organizationName_default = ACME Corp.
organizationalUnitName_default = dev
emailAddress_default = dev@acme.com
localityName_default = Gotham City
stateOrProvinceName_default = DC
countryName_default = US
commonName_default = acme

[ v3_ca ]
basicConstraints = CA:TRUE
subjectKeyIdentifier = hash
authorityKeyIdentifier = keyid:always,issuer:always

[ v3_req ]
basicConstraints = CA:FALSE
subjectKeyIdentifier = hash
EOF

yes "$(printf '\n')" \
  | openssl req -new -x509 -extensions v3_ca -keyout ca.key -out ca.crt -days 3650 \
      -config ./openssl.cnf --passout "pass:${CA_CERT_DEV_PASSWORD}"

openssl x509 -in ca.crt -pubkey -noout > ca.pub

yes "$(printf '\n')" \
  | openssl req -new -nodes -out req.pem -config ./openssl.cnf

yes \
  | openssl ca -passin "pass:${CA_CERT_DEV_PASSWORD}" -out dev.crt \
      -config ./openssl.cnf -infiles req.pem

openssl x509 -in dev.crt -pubkey -noout > dev.pub
```
