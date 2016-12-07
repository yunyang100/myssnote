# Myssnote

This note is to document how to set up ss server.

# install the ss
--apt-get install python-pip <br>
--pip install shadowsocks

####Maybe you need to upgrade the pip or install the setuptools
--pip install -U pip      // -U  upgrade <br>
--apt-get install python-setuptools

# Start
--ssserver -p 443 -k password -m rc4-md5<br>
ssserver -p server_port -k yourPassword -m Method

# To run in the backgorund
--sudo ssserver -p 443 -k password -m rc4-md5 --user nobody -d start<br>
ssserver -p server_port -k yourPassword -m Method --user Username -d run in the background

# Stop
--sudo ssserver -d stop

# Shadowsocks configuration may be done with a JSON formatted file.You can create a config.json and put it to /etc/shadowsocks
{<br>
    "server":"my_server_ip",    
    "server_port":8388,    
    "local_address": "127.0.0.1",    
    "local_port":1080,    
    "password":"mypassword",    
    "timeout":300,    
    "method":"aes-128-ctr",    
    "fast_open": false,    
    "workers": 1<br>
}<br>
from https://wiki.archlinux.org/index.php/Shadowsocks

# To start it in the foreground using the configuration file /etc/shadowsocks/config.json:
--$ ssserver -c /etc/shadowsocks/config.json

# To run in the background:
$ ssserver -c /etc/shadowsocks/config.json -d start<br>
$ ssserver -c /etc/shadowsocks/config.json -d stop
