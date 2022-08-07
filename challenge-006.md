Ping automatization
===
Create a `cron` task on the machine running node validator that allows ping to network automatically.

### Steps
* Create a new file on `/home/<USER_ID>/scripts/ping.sh`
> **&#60;USER_ID&#62;** — username

```
#!/bin/sh
# Ping call to renew Proposal added to crontab
export NEAR_ENV=shardnet
export LOGS=/home/<USER_ID>/logs
export POOLID=<YOUR_POOL_ID>
export ACCOUNTID=<YOUR_ACCOUNT_ID>
echo "---" >> $LOGS/all.log
date >> $LOGS/all.log
near call $POOLID.factory.shardnet.near ping '{}' --accountId $ACCOUNTID.shardnet.near --gas=300000000000000 >> $LOGS/all.log
near proposals | grep $POOLID >> $LOGS/all.log
near validators current | grep $POOLID >> $LOGS/all.log
near validators next | grep $POOLID >> $LOGS/all.log
```

* Create logs folder:
```
mkdir $HOME/logs
```

* Change execute permission for `ping.sh` file:
```
chmod +x $HOME/scripts/ping.sh
```

* Create a new `crontab`, running every 2 hours:
```
crontab -e
0 */2 * * * sh /home/<USER_ID>/scripts/ping.sh
```

* List `crontab` to see it is running:
```
crontab -l
```

* Review your logs:
```
cat $HOME/logs/all.log
```

**Logs example:**
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-006/1.png)

**Ping example:**
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-006/2.png)

**Link to our account:**
<https://explorer.shardnet.near.org/accounts/btcsecure.shardnet.near>
***
⏪[Challenge 005](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-005.md)     | [Challenge 007](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-007.md)⏩
---|---:
