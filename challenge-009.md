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
⏪[Challenge 008](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-008.md)     | [Challenge 013](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-013.md)⏩
:---|---:
