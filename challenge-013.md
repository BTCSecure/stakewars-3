# Backup node

In case of missed blocks or chunks, the validator can be 
removed from the active validation set in the next auction. If you want 
to secure your validator NEAR node from a high downtime, you can deploy a
 **backup** server with the preconfigured NEAR node. Having
 two provisioned nodes allows you to quickly switch from one server to 
another by migrating your validator keys, so you can continue producing 
blocks with minimal downtime. If the nearcore release has long database 
migration, or you must maintain/scale the server, we also recommend 
migrating your validator keys to the backup node.

Always analyze your node activities and be ready to determine a problem and move the *main validator* keys to the **backup** node.

### Validator keys migration

Firstly, you need to have a backup server, a NEAR node with a new `node_key.json` and one more generated `validator_key.json`. To switch quickly, prepare folders for the validator keys and reserve keys

⚠️ **Be careful! Don't let two nodes run with the same keys!
This will make your node slashed. This means that your node will be 
excluded from the active validation set and your funds may be burnt.**

If the server is **unavailable** (e.g. no network connection) deal with the hosting provider, get access and **only** then start the key migration procedure! Always make sure that the **MAIN** node doesn’t work

If the server is **available**

1. Stop the **MAIN** node

```
sudo systemctl stop neard
```

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-013/ch13-main-001-1.png)

2. Make sure the **MAIN** node isn’t working

```
ps aux | grep neard
netstat -tlpn | grep neard
```

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-013/ch13-main-002-1.png)

3. Copy files from **MAIN** node to **RESERVE** node

```
sudo scp <USER>@<MAIN_NODE_IP_ADDR>:<WORKDIR>/.near/node_key.json <WORKDIR>/.near-primary/
sudo scp <USER>@<MAIN_NODE_IP_ADDR>:<WORKDIR>/.near/validator_key.json <WORKDIR>/.near-primary/
sudo chown -R <USER>:<USER> <WORKDIR>/.near-primary/
```

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-013/ch13-backup-001-2.png)

4. Replace main validator keys on the **MAIN** node with the reserve ones (optional, if you are sure the node won’t start accidentally)

```
cd ~/.near
rm validator_key.json node_key.json
cp ~/.near-secondary/node_key.json ~/.near-secondary/validator_key.json ~/.near/
```

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-013/ch13-main-003-1.png)

Stop the **BACKUP** node

```
sudo systemctl stop neard
```

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-013/ch13-backup-002-1.png)

5. Make sure the **BACKUP** node isn’t workin

```
ps aux | grep neard
netstat -tlpn | grep neard
```

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-013/ch13-backup-003-1.png)

6. Replace reserve keys on the **BACKUP** node with main validator

```
cd ~/.near
rm validator_key.json node_key.json
cp ~/.near-primary/node_key.json ~/.near-primary/validator_key.json ~/.near/
```

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-013/ch13-backup-004-1.png)

7. Check the `validator_key.json` and `node_key.json`

You can check file identity using `md5sum` command for `validator_state.json` and `node_key.json` on both nodes. If the checksums match, then the files are identical.

Or you use `diff` command

```
diff <WORK_DIR>/.near/validator_key.json ../<RESERVE_KEYS>/validator_key.json
diff <WORK_DIR>/.near/node_key.json ../<RESERVE_KEYS>/node_key.json

diff <WORK_DIR>/.near/validator_key.json ../<VALIDATOR_KEYS>/validator_key.json
diff <WORK_DIR>/.near/node_key.json ../<VALIDATOR_KEYS>/node_key.json
```

8. Start the **BACKUP** node

```
sudo systemctl start neard
```

After starting the node in the log, you **used to see** the line with `peer_id` that was equal to `public_key` in `/<WORK_DIR>/.near/node_key.json` & `../<VALIDATOR_KEYS>/node_key.json`, **but now just make sure that your backup node is validating**.
In the logs of the **BACKUP** node you should see "Validator |"

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-013/ch13-backup-005-1.png)

**Our example for backup node:**

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-013/ch13-backup-005-final.png)
