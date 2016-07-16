# axis2c-trunk
Mirror of axis2/c

#Ubuntu 14.04-LTS

```
sudo apt-get install libjson0-dev 

./autogen.sh
./configure --enable-openssl=yes --with-openssl=/usr/include/openssl --disable-libxml2 --enable-guththila=yes --enable-json=yes --enable-trace=yes --enable-tcp --with-json="/usr/include/json-c"

make && make install
```
