This is my fork of Effi's Tor exit node script.

https://github.com/juhanurmi/exitnode

```sh
sudo bash remove.sh
sudo apt-get update && sudo apt-get upgrade
sudo rpi-update
sudo apt-get install haveged
sudo apt-get install tor
sudo cp torrc /etc/tor/torrc
sudo cp tor-exit-notice.html /etc/tor/tor-exit-notice.html
sudo cp sysctl.conf /etc/sysctl.conf
sudo cp rules.v4 /etc/iptables/rules.v4
sudo apt-get install iptables-persistent
sudo modprobe ip_conntrack
sudo echo "ip_conntrack" >> /etc/modules
sudo service iptables-persistent restart
sudo sysctl -p /etc/sysctl.conf
sudo service tor restart
# After installation may be good idea to
sudo reboot
```

# Troubleshooting

Is entropy level too low (<1000)?
```sh
python -c "$(echo -e "import time\nwhile True:\n time.sleep(1)\n print open('/proc/sys/kernel/random/entropy_avail', 'rb').read(),")"
```

# How much Tor is consuming CPU?

```sh
top -sp <tor_pid>
```

# Too many TCP connections?

```sh
netstat -tn | wc -l
ulimit -n
# Try this if you have problems
ulimit -n 20000
```
