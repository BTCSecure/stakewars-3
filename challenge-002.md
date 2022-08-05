Настройка ноды
===
* Перед началом работы убедимся, что наша машина имеет нужные характеристики:
```
lscpu | grep -P '(?=.*avx )(?=.*sse4.2 )(?=.*cx16 )(?=.*popcnt )' > /dev/null \
  && echo "Supported" \
  || echo "Not supported"
```
> Supported — Поддерживается

* Устанавливаем инструменты разработчика:
```
sudo apt install -y git binutils-dev libcurl4-openssl-dev zlib1g-dev libdw-dev libiberty-dev cmake gcc g++ python docker.io protobuf-compiler libssl-dev pkg-config clang llvm cargo
```

* Если вы столкнулись с проблемами во время установки **python** или **docker.io** на **Ubuntu**, выполните следующую команду:
```
sudo apt install python3
sudo apt install docker-ce
```

* Установка **Python pip**:
```
sudo apt install python3-pip
```

* Настройка конфигурации:
```
USER_BASE_BIN=$(python3 -m site --user-base)/bin
export PATH="$USER_BASE_BIN:$PATH"
```

* Установка **Building env**:
```
sudo apt install clang build-essential make
```

* Установка **Rust & Cargo**:
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

При установке увидим следующее:    | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-002/1.png)
------------------------------------|-----------------------------------------------------------------------------------
> **Выбираем 1 и нажимаем Enter**

* Выполняем команду:
```
source $HOME/.cargo/env
```

* Клонируем репозиторий [nearcore](https://github.com/near/nearcore):
```
git clone https://github.com/near/nearcore
cd nearcore
git fetch
```

* Для актуального коммита пройди по [этой ссылке](https://github.com/near/stakewars-iii/blob/main/commit.md). Далее переходим к необходимому коммиту:
```
git checkout <commit>
```

* В папке `nearcore` запускаем следующие команды:
```
cargo build -p neard --release --features shardnet
```

Компиляция бинарника `nearcore` может занять некоторое время     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-002/2.png)
-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------
***
* Для правильной работы ноды NEAR требуется рабочий каталог и несколько конфигурационных файлов. Создаем начальный рабочий каталог, выполнив команду:
```
./target/release/neard --home ~/.near init --chain-id shardnet --download-genesis
```
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-002/3.png)
> Эта команда создаст структуру каталогов и сгенерирует `config.json`, `node_key.json`, и `genesis.json`.
* `config.json` — Параметры конфигурации, которые отвечают за то, как будет работать узел. В config.json содержится необходимая информация о том, как узел будет работать в сети, как общаться с пирами, и как достигать консенсуса. Некоторые параметры могут настраиваются. В целом, валидаторы предпочитают использовать предоставленный config.json как есть, т.е. по умолчанию.
* `genesis.json` — Файл со всеми данными, с которыми начиналась сеть в момент генезиса. Он содержит начальные счета, контракты, ключи доступа и другие записи, которые представляют собой начальное состояние блокчейна. Файл `genesis.json`  это снимок состояния сети в определенный момент времени. В нем содержатся контакты счетов, балансы, активные валидаторы и другая информация о сети.
* `node_key.json` — Файл, содержащий открытый и закрытый ключ для ноды. Также включает необязательный параметр `account_id`, который требуется для запуска ноды валидатора (не рассматривается в данном документе).
* `data/` — Папка, в которую узел NEAR будет записывать свое состояние.
***
В сгенерированном `config.json` есть два параметра, которые необходимо изменить:
* `boot_nodes`: Если вы не указали загрузочные ноды, сгенерированный `config.json` покажет пустой массив, поэтому нам нужно будет заменить его на полный массив с указанием загрузочных нод.
* `tracked_shards`: Это поле будет пустым, в сгенерированном файле `config.json`. Нам нужно заменить его на `"tracked_shards": [0]`
```
rm ~/.near/config.json
wget -O ~/.near/config.jsonhttps://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/config.json
```
***
* Следующим шагом запускаем ноду:
```
cd ~/nearcore
./target/release/neard --home ~/.near run
```
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-002/4.png)
**Теперь нода запущена, и вы можете видеть логи в консоли. Ваша нода должна найти пиры, загрузить хедеры до 100%, а затем загружать блоки.**
***
Становимся валидатором
===
Для подписания транзакций через **NEAR-CLI** необходимо установить полный ключ доступа, а для этого нужно авторизоваться в кошельке на локальном уровне.

* Выполняем команду, которая запустит веб-браузер, позволяя разрешить копирование ключа полного доступа:

`near login`     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-002/5.png)
:---:|---
**Даем доступ NEAR-CLI:**     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-002/6.png)
**После предоставления доступа мы увидим такую страницу:**     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-002/7.1.png)
**Или такую:**     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-002/7.2.png)
**Возвращаемся в консоль, вводим имя своего кошелька, если это не произошло автоматически и нажимаем Enter:**     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-002/8.png)

* Проверяем файл `validator_key.json` командой:
```
cat ~/.near/validator_key.json
```

Если файл `validator_key.json` отсутствует, выполняем следующие шаги для его создания:
* Генерируем ключ пула
```
near generate-key <pool_id>
```
> <pool_id> — ***xx.factory.shardnet.near***, где ***'хх'*** имя нашего пула
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-002/9.png)

* Копируем сгенерированный файл в папку `shardnet`. Убеждаемся, что заменили `<pool_id>` на наш `account_id`
```
cp ~/.near-credentials/shardnet/YOUR_WALLET.json ~/.near/validator_key.json
```

* Меняем `account_id` => `xx.factory.shardnet.near`, где ***xx*** имя нашего пула
* Меняем `private_key` на `secret_key`
> **`account_id` должен совпадать с именем контракта стейкинг пула, иначе мы не сможем подписывать блоки**

Содержимое файла должно иметь следующий вид:
```
{
  "account_id": "xx.factory.shardnet.near",
  "public_key": "ed25519:HeaBJ3xLgvZacQWmEctTeUqyfSU4SDEnEwckWxd92W2G",
  "secret_key": "ed25519:****"
}
```

* Запускаем ноду валидатора как сервис:
```
sudo vi /etc/systemd/system/neard.service
```

* Вставляем:
```
[Unit]
Description=NEARd Daemon Service
[Service]
Type=simple
User=<USER>
#Group=near
WorkingDirectory=/home/<USER>/.near
ExecStart=/home/<USER>/nearcore/target/release/neard run
Restart=on-failure
RestartSec=30
KillSignal=SIGINT
TimeoutStopSec=45
KillMode=mixed
[Install]
WantedBy=multi-user.target
```
> Где &#60;USER&#62; — имя нашего пользователя.

* Команда активации сервиса:
```
sudo systemctl enable neard
```

* Команда запуска сервиса:
```
sudo systemctl start neard
```

* Если нам нужно внести изменения в сервис из-за ошибки в файле, то его необходимо перезагрузить:
```
sudo systemctl reload neard
```

* Посмотреть логи работы ноды можно следующей командой:
```
journalctl -n 100 -f -u neard
```

* А чтобы логи имели человеческий вид, выполняем команду:
```
sudo apt install ccze
```

* Далее пишем команду:
```
journalctl -n 100 -f -u neard | ccze -A
```

* Любуемся результатом:
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-002/10.png)
***
### Условия, которые необходимо выполнить, прежде чем стать валидатором:
* Нода должна быть полностью синхронизирована;
* Файл `validator_key.json` должен быть на своем месте;
* Контракт должен быть инициализирован `public_key` в `validator_key.json`;
* `account_id` должен быть установлен `id` контрактом стейкинг пула;
* Должно быть достаточно делегировано, чтобы удовлетворить минимальную стоимость места. Ознакомиться с ценой места можно [здесь](https://explorer.shardnet.near.org/nodes/validators);
* Предложение должно быть подтверждено “пингуя” контракт;
* После принятия предложения валидатор должен подождать 2–3 эпохи, чтобы войти в набор валидаторов;
* Став валидатором, валидатор должен производить более 90% назначенных блоков.

#### Проверьте статус работы ноды валидатора. Если отображается “Validator”, значит ваш пул стал валидатором.
***
⏪[Challenge 001](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-001.md)     | [Challenge 003](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-003.md)⏩
---|---:
