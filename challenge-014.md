# Part I. 

## Auto-backup node

A backup node is a separate server for taking and storing database snapshots.
This is necessary, for example, to quickly transfer an up-to-date 
database to another server so that the new node is synchronized as 
quickly as possible, or to restore a damaged database

⚠️ Be aware that it takes time to copy the database. Do not use an auto-backup script on the validator node!

Example `backup.sh`**:**

```
#!/bin/bash

DATE=$(date +%Y-%m-%d-%H-%M)
DATADIR=/home/test
BACKUPDIR=/home/test/backups/near_${DATE}

mkdir $BACKUPDIR

sudo systemctl stop neard

wait

echo "NEAR node was stopped" | ts

if [ -d "$BACKUPDIR" ]; then
    echo "Backup started" | ts

    cp -rf $DATADIR/.near/data/ ${BACKUPDIR}/

    # Submit backup completion status, you can use healthchecks.io, betteruptime.com or other services
    # Example
    # curl -fsS -m 10 --retry 5 -o /dev/null https://hc-ping.com/xXXXxXXx-XxXx-XXXX-XXXx-...

    echo "Backup completed" | ts
else
    echo $BACKUPDIR is not created. Check your permissions.
    exit 0
fi

sudo systemctl start neard

echo "NEAR node was started" | ts
```
### How it works:

![ch14-backup-001-1.png](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-014/ch14-backup-001-1.png)

### Backup files:

![ch14-backup-001-2.png](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-014/ch14-backup-001-2.png)

### For an automatic start:

```
sudo nano /etc/crontab
```

- **Add line:**

```
# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name command to be executed
0  12 *  *  * near      /home/test/scripts/backup.sh >> /home/test/backups/backup.log 2>&1
```

### Example:

![ch14-backup-002-1.png](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-014/ch14-backup-002-1.png)

💡 This setting will automatically start database backup every day at 12:00

# Part II.

Try to make a backup on your backup node, and modify the auto-backup script :

- Save the data folder as an archive
- Check the folder with backups and remove the oldest
- Write a simple script for quick database restoring

## Let’s modify backup script:

```
#!/bin/bash

DATE=$(date +%Y-%m-%d-%H-%M)
DATADIR=/home/test/.near
BACKUPDIR=/home/test/backups

sudo systemctl stop neard

wait

echo "NEAR node was stopped" | ts

if [ -d "$BACKUPDIR" ]; then
    echo "Deleting old backups was started" | ts
    rm ${BACKUPDIR}/near_*
    echo "Deleting completed" | ts
    echo "Backup started" | ts
    cd ${DATADIR}
    tar cf ${BACKUPDIR}/near_${DATE}.tar data

    echo "Backup completed" | ts
else
    echo Something went wrong. Check your permissions.
    exit 0
fi

sudo systemctl start neard
echo "NEAR node was started" | ts
```

### How it works:

![ch14-backup-003-1.png](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-014/ch14-backup-003-1.png)

## Let’s write a simple script for quick database restoring:

```
#!/bin/bash
DATADIR=/home/test/.near
BACKUPDIR=/home/test/backups

sudo systemctl stop neard
wait
echo "NEAR node was stopped" | ts

    echo "Deleting olf files in data folder was started" | ts
    rm -R ${DATADIR}/data/*
    echo "Deleting completed" | ts
    echo "Restoring started" | ts
    cd ${DATADIR}
    tar xf ${BACKUPDIR}/near_*.tar
    echo "Restoring completed" | ts

sudo systemctl start neard
echo "NEAR node was started" | ts
```

### How it works with a backup script:

![ch14-backup-004-1.png](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-014/ch14-backup-004-1.png)
***
⏪[Challenge 013](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-013.md)     | [Challenge 019](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-019.md)⏩
:---|---:
