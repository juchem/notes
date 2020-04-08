# general debugging
- logs: `/var/log/mysql/error.log`
- debug with telnet: ```
  $ telnet example.com 3306
  Trying 255.0.0.71...
  Connected to example.com.
  Escape character is '^]'.
  FHost '255.0.0.70' is not allowed to connect to this MySQL serverConnection closed by foreign host.
  ```

# simple dev settings
- localhost access only: ```
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON database_name.table_name TO 'username'@'localhost';
```
- access from any host: ```
CREATE USER 'username'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON database_name.table_name TO 'username'@'%';
```
- note: `database_name` and `table_name` can be `\*` (no quotes needed)


# SQL Error (2013): Lost connection to MySQL server at 'reading inital communication packet', system error:0
- check that the bind address on `/etc/mysql/my.cnf` is accepts the address
  used by the client
- check that `/etc/ssh/sshd_config` has `AllowTcpForwarding yes` (seems to be
  default) otherwise packets will be silently dropped by ssh.
