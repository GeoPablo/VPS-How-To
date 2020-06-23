# Notes

### Show in use ports on machine

`sudo netstat -tulpn | grep LISTEN`

### To make app only available from the internal host

use a host with value 127.0.0.1

_NodeJS example_
`app.listen(3000,127.0.0.1)`
