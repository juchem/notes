# encrypt
- python 3 (requires package `python3-bcrypt` in debian):
```
$ PLAIN_TEXT="the string to encrypt"
$ python3 <<EOF
import bcrypt
print(bcrypt.hashpw(b'${PLAIN_TEXT}', bcrypt.gensalt()).decode('ascii'))
EOF
```
