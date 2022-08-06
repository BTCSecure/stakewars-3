Автоматизация пинга
===
Создаем задачу `cron` на машине, на которой запущен валидатор, которая позволяет автоматически пинговать сеть.

### Шаги
* Создаем новый файл по пути `/home/<USER_ID>/scripts/ping.sh`
> Где **&#60;USER_ID&#62;** — имя вашего пользователя

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

* Создаем папку, где будут храниться логи:
```
mkdir $HOME/logs
```

* Изменяем разрешение на выполнение для файла `ping.sh`:
```
chmod +x $HOME/scripts/ping.sh
```

* Создаем новый `crontab`, запускаемый каждые 2 часа:
```
crontab -e
0 */2 * * * sh /home/<USER_ID>/scripts/ping.sh
```

* Посмотреть работает ли `crontab`, можно этой командой:
```
crontab -l
```

* Посмотреть логи можно тут:
```
cat $HOME/logs/all.log
```

**Пример логов:**
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-006/1.png)

**Пример работы пинга:**
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-006/2.png)

Ссылка на наш аккаунт:

<https://explorer.shardnet.near.org/accounts/btcsecure.shardnet.near>
***
⏪[Challenge 005](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-005.md)     | [Challenge 007](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-007.md)⏩
---|---:
