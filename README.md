# This is a fork!
## Full credit goes to the original authors, please refer to the original source at https://github.com/furlongm/openvpn-monitor


# OpenVPN-Monitor


## Summary

OpenVPN-Monitor is a simple python program to generate html that displays the
status of an OpenVPN server, including all current connections. It uses the
OpenVPN management console. It typically runs on the same host as the OpenVPN
server, however it does not necessarily need to.

[![](https://raw.githubusercontent.com/furlongm/openvpn-monitor/gh-pages/screenshots/openvpn-monitor.png)](https://raw.githubusercontent.com/furlongm/openvpn-monitor/gh-pages/screenshots/openvpn-monitor.png)


## Source

The current source code is available on github:

https://github.com/furlongm/openvpn-monitor


## Installation with virtualenv + pip + gunicorn

Installation on Amazon Linux is a pain, you will have to manually resolve some dependencies.

```shell
mkdir /srv/openvpn-monitor
cd /srv/openvpn-monitor
virtualenv venv
. venv/bin/activate
pip install openvpn-monitor gunicorn
pip install -r requirements.txt
gunicorn openvpn-monitor -b 0.0.0.0:80
```


### Checkout OpenVPN-Monitor

```shell
cd /var/www/html
git clone https://github.com/furlongm/openvpn-monitor.git
```


### Configure OpenVPN

Add the following line to your OpenVPN server configuration to run the
management console on 127.0.0.1 port 5555:

```
management 127.0.0.1 5555
```

Refer to the OpenVPN documentation for further information on how to secure
access to the management interface.


### Download the GeoLite City database

```shell
cd /usr/share/GeoIP/
wget http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz
gunzip GeoLiteCity.dat.gz
mv GeoLiteCity.dat GeoIPCity.dat
```


### Configure OpenVPN-Monitor

The example configuration file `/var/www/html/openvpn-monitor/openvpn-monitor.conf`
should give some indication of how to set site name, add a logo, etc. You can
also set a default location (latitude and longitude) for the embedded maps.
If not set, the default location is Melbourne, Australia.

Edit `/opt/virtualenvs/openvpn-monitor/venv/etc/openvpn-monitor.conf` to match your site.

You should now be able to navigate to `http://myipaddress/openvpn-monitor`


### Debugging

OpenVPN-Monitor can be run from the command line in order to test if the html
generates correctly:

```shell
cd /var/www/html/openvpn-monitor
python openvpn-monitor.py
```

Further debugging can be enabled by specifying the `--debug` flag:

```shell
cd /var/www/html/openvpn-monitor
python openvpn-monitor.py -d
```


## License

OpenVPN-Monitor is licensed under the GPLv3, a copy of which can be found in
the COPYING file.


## Acknowledgements

Flags are created by Matthias Slovig (flags@slovig.de) and are licensed under
Creative Commons License Deed Attribution-ShareAlike 3.0 Unported
(CC BY-SA 3.0). See http://flags.blogpotato.de/ for more details.
