# Uptime monitor
* Check your current uptime and manage it to above 70% on ShardNet
* Fix issues with producing chunks.
See the [troubleshooting guide](https://github.com/near/stakewars-iii/blob/main/challenges/troubleshooting.md)
* Implement monitoring scripts
### Open Port 3030 for Diagnostic reporting

* Check to see if PORT 3030 is open:

```
sudo iptables -L | grep 3030
```

* Open the port if not open:

```
sudo iptables -A INPUT -p tcp --dport 3030 -j ACCEPT
```

**Save the config for server restarts. You can use one of the 2 solutions:**

#### 1. Using `iptables-persistent`:
* Command

```
sudo apt install iptables-persistent
```

* Or if already installed

```
sudo dpkg-reconfigure iptables-persistent
```

#### 2. Using files:
```
iptables-save > /etc/iptables/rules.v4
ip6tables-save > /etc/iptables/rules.v6
```
***
### Validate the port is open by visiting:
[http://<NODE_IP>:3030/status](http://<NODE_IP>:3030/status)
> **<NODE_IP>** — ip-address of your node.
> 
> ***NOTE**: In some cases the port may also need to be opened in your cloud provider / datacenter firewall.*

#### btcsecure: <http://65.109.22.107:3030/status>
#### leaderboard: <https://openshards.io/shardnet-uptime-scoreboard/>

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-009/21-Leaderboard.png)
***
⏪[Challenge 008](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-008.md)     | [Оглавление](https://github.com/BTCSecure/stakewars-3#%D0%BF%D0%BE%D1%88%D0%B0%D0%B3%D0%BE%D0%B2%D0%B0%D1%8F-%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%86%D0%B8%D1%8F-%D0%BF%D0%BE-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D1%83-%D0%B2%D0%B0%D0%BB%D0%B8%D0%B4%D0%B0%D1%82%D0%BE%D1%80%D0%B0)⏩
:---|---:
