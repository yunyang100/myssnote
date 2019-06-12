# MyssMote

This note is to document how to set up ss server.

# Install the ss
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
$ ssserver -c /etc/shadowsocks.json -d start<br>
$ ssserver -c /etc/shadowsocks.json -d stop

#EVP_CIPHER_CTX_cleanup错误<br>
用vim打开文件：vim /usr/local/lib/python2.7/dist-packages/shadowsocks/crypto/openssl.py (该路径请根据自己的系统情况自行修改，如果不知道该文件在哪里的话，可以使用find命令查找文件位置)<br>
跳转到52行（shadowsocks2.8.2版本，其他版本搜索一下cleanup）<br>
进入编辑模式<br>
将第52行libcrypto.EVP_CIPHER_CTX_cleanup.argtypes = (c_void_p,) <br>
改为libcrypto.EVP_CIPHER_CTX_reset.argtypes = (c_void_p,)<br>
再次搜索cleanup（全文件共2处，此处位于111行），将libcrypto.EVP_CIPHER_CTX_cleanup(self._ctx) <br>
改为libcrypto.EVP_CIPHER_CTX_reset(self._ctx)<br>
保存并退出<br>
启动即可
