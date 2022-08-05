Мониторинг
===
### Логи
Файл журнала хранится либо в каталоге `~/.nearup/logs`, либо в `systemd`, в зависимости от вашей настройки.
* Команда Systemd:
```
journalctl -n 100 -f -u neard | ccze -A
```
* Пример лога:
Validator | 1 validator
```
INFO stats: #85079829 H1GUabkB7TW2K2yhZqZ7G47gnpS7ESqicDMNyb9EE6tf Validator | 73 validators 30 peers ⬇ 506.1kiB/s ⬆ 428.3kiB/s 1.20 bps 62.08 Tgas/s CPU: 23%, Mem: 7.4 GiB
```
> - **Validator**: означает, что вы являетесь активным валидатором
> - **73 validators**: всего 73 валидатора в сети
> - **30 peers**: в настоящее время у вас 30 пиров. Для достижения консенсуса и начала валидирования вам нужно не менее 3 пиров.
> - **#46199418**: номер блока — убедитесь, что блоки двигаются
***
### RPC
Любая нода в сети предоставляет RPC сервисы на порту 3030, если порт открыт в брандмауэре ноды. NEAR-CLI использует вызовы RPC за кулисами. Обычно RPC используется для проверки статистики валидатора, версии ноды и просмотра доли делегата, хотя он может использоваться для взаимодействия с блокчейном, счетами и контрактами в целом.

Более подробно о многих командах и о том, как их использовать, можно узнать [здесь](https://docs.near.org/api/rpc/introduction).

* Команда:
```
sudo apt install curl jq
```

* Команда проверки версии ноды:
```
curl -s http://127.0.0.1:3030/status | jq .version
```

* Команда для проверки делегатов и стейка:
```
near view <your pool>.factory.shardnet.near get_accounts '{"from_index": 0, "limit": 10}' --accountId <accountId>.shardnet.near
```

* Команда, чтобы узнать причину кика валидатора:
```
curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' 127.0.0.1:3030 | jq -c '.result.prev_epoch_kickout[] | select(.account_id | contains ("<POOL_ID>"))' | jq .reason
```

* Команда, чтобы узнать сколько блоков произведено к ожидаемому количеству блоков:
```
curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json'http://localhost:3030/ | jq -c '.result.current_validators[] | select(.account_id | contains ("<POOLID>"))'
```
***
Подключение мониторинга
===
Рассмотрим получение необходимых уведомлений в телеграм на базе очень простого скрипта, cуть которого заключается в том, чтобы сигнализировать нам о падающем онлайне ноды и сообщать кол-во пропущенных блоков за текущую эпоху.

Для начала нам нужно приобрести новый сервер, на котором будет выполняться скрипт, особых требований к серверу не будет.

* После покупки необходимо сервер настроить, для этого, в первую очередь, убедимся, что он обновлен:
```
sudo apt update && sudo apt upgrade -y
```

Далее устанавливаем `curl`, `jq` и `bc`:
```
sudo apt install curl jq bc -y
```
***
Теперь переходим в телеграм и создаем бота. Отправляемся сюда —  <https://t.me/BotFather> и выполняем следующие шаги:
* В чате пишем команду `/newbot`;
* Указываем желаемое имя для бота;
* Получаем токен в формате: `5580205772:AABBtKj31FtYcpTvbx-hXFPCJVs2eEmk7wg`, это и будет наш &#60;TOKEN&#62;.

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-004/16-new_bot.png)

Теперь переходим к этому боту <https://t.me/getmyid_bot> и пишем следующее:
* `/start`
* Получаем ID в формате: `2345234230`, это и будет наш &#60;CHAT_ID&#62;.
***
* Возвращаемся к серверу и создаём папку, где будет расположен будущий скрипт:
```
mkdir ~/scripts
cd ~/scripts
```

* Создаем скрипт:
```
nano nearalerts.sh
```

* Вставляем в файл данный текст:
```
#!/bin/bash
TOKEN=<TOKEN>
CHAT_ID=<CHAT_ID>
URL=”https://api.telegram.org/bot$TOKEN/sendMessage"
QUERY=`curl -s -d ‘{“jsonrpc”: “2.0”, “method”: “validators”, “id”: “dontcare”, “params”: [null]}’ -H ‘Content-Type: application/json’ http://<NODE_IP>:3030/ | jq -c ‘.result.current_validators[] | select(.account_id | contains (“<POOL_ID>”))’`
EXPECTED=`echo $QUERY | sed -e ‘s/.*num_expected_chunks..//g; s/..num_produced_blocks.*//g’`
PRODUCED=`echo $QUERY | sed -e ‘s/.*num_produced_chunks..//g; s/..public_key.*//g’`
ONLINE=$(bc<<<”scale=4;$PRODUCED/$EXPECTED*100")
PAR1=”70.0000"
PAR2=$(( $EXPECTED-$PRODUCED ))
if (( $(echo “$ONLINE < $PAR1” |bc -l) ));
 then
 MESSAGE=”Онлайн валидатора: $ONLINE%, пропущено блоков: $PAR2.”
 curl -s -X POST $URL -d chat_id=$CHAT_ID -d text=”$MESSAGE”
 else
 sleep 1
fi
echo
```
> Где:
> - **&#60;TOKEN&#62;:** это токен нашего бота в телеграме;
> - **&#60;CHAT_ID&#62;:** это id чата, куда будут приходить уведомления от бота;
> - **&#60;NODE_IP&#62;:** ip адрес ноды валидатора;
> - **&#60;POOL_IP&#62;:** имя пула валидатора.

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-004/15-script.png)

* Делаем этот скрипт исполняемым:
```
sudo chmod -x /home/<USER>/scripts/nearalerts.sh
```

* Следующим шагом нам необходимо сделать так, чтобы этот скрипт включался каждые 5 минут, для этого создаем задачу в кроне:
```
crontab -e
```

* Далее вставляем эту строчку:
```
*/5 * * * * /home/<USER_ID>/scripts/nearalerts.sh
```
> Где **&#60;USER&#62;**: имя твоего пользователя.

* Проверяем работу:
```
crontab -l
```

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-004/17-complete.png)

#### На этом настройка скрипта завершена.
***
⏪[Challenge 003](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-003.md)     | [Challenge 005](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-005.md)⏩
---|---:
