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

![main-001-1.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/53de9acc-98b6-44de-a4ff-394766f19b3c/main-001-1.png)

1. Make sure the **MAIN** node isn’t working

```
ps aux | grep neard
netstat -tlpn | grep neard
```

![main-002-1.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/92ae6198-4697-4689-b027-24a46c110987/main-002-1.png)

1. Copy files from **MAIN** node to **RESERVE** node

```
sudo scp <USER>@<MAIN_NODE_IP_ADDR>:<WORKDIR>/.near/node_key.json <WORKDIR>/.near-primary/
sudo scp <USER>@<MAIN_NODE_IP_ADDR>:<WORKDIR>/.near/validator_key.json <WORKDIR>/.near-primary/
sudo chown -R <USER>:<USER> <WORKDIR>/.near-primary/
```

![backup-001-2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6378a9db-7ac2-4abf-8f7b-d07b34f43d58/backup-001-2.png)

1. Replace main validator keys on the **MAIN** node with the reserve ones (optional, if you are sure the node won’t start accidentally)

```
cd ~/.near
rm validator_key.json node_key.json
cp ~/.near-secondary/node_key.json ~/.near-secondary/validator_key.json ~/.near/
```

![main-003-1.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a43fa2b1-56fb-4ca1-bd71-9558c14075ce/main-003-1.png)

Stop the **BACKUP** node

```
sudo systemctl stop neard
```

![backup-002-1.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d4a5b80-4f7c-4693-916c-846b53374595/backup-002-1.png)

1. Make sure the **BACKUP** node isn’t workin

```
ps aux | grep neard
netstat -tlpn | grep neard
```

![backup-003-1.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f320315a-1899-416b-92d6-c343d8d39bd6/backup-003-1.png)

1. Replace reserve keys on the **BACKUP** node with main validator

```
cd ~/.near
rm validator_key.json node_key.json
cp ~/.near-primary/node_key.json ~/.near-primary/validator_key.json ~/.near/
```

![backup-004-1.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0dd2265f-af80-4d33-bb59-736e12620509/backup-004-1.png)

1. Check the `validator_key.json` and `node_key.json`

You can check file identity using `md5sum` command for `validator_state.json` and `node_key.json` on both nodes. If the checksums match, then the files are identical.

Or you use `diff` command

```
diff <WORK_DIR>/.near/validator_key.json ../<RESERVE_KEYS>/validator_key.json
diff <WORK_DIR>/.near/node_key.json ../<RESERVE_KEYS>/node_key.json

diff <WORK_DIR>/.near/validator_key.json ../<VALIDATOR_KEYS>/validator_key.json
diff <WORK_DIR>/.near/node_key.json ../<VALIDATOR_KEYS>/node_key.json
```

1. Start the **BACKUP** node
    
    ```
    sudo systemctl start neard
    ```
    

After starting the node in the log, you **used to see** the line with `peer_id` that was equal to `public_key` in `/<WORK_DIR>/.near/node_key.json` & `../<VALIDATOR_KEYS>/node_key.json`, **but now just make sure that your backup node is validating**.
In the logs of the **BACKUP** node you should see "Validator |"

![backup-005-1.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/41e69e53-066b-4108-8c9f-adcc240826ce/backup-005-1.png)

**Our example for backup node:**

![backup-005-final.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b7565f70-6c79-4c9d-8079-b1306bed74c7/backup-005-final.png)
