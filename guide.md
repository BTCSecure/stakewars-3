# Пошаговая инструкция по запуску валидатора в сети ShardNet
* [Покупка VPS](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%BF%D0%BE%D0%BA%D1%83%D0%BF%D0%BA%D0%B0-vps)
* [Создание кошелька](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BA%D0%BE%D1%88%D0%B5%D0%BB%D1%8C%D0%BA%D0%B0)
* [Установка NEAR-CLI](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-near-cli)
* [Настройка ноды](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%BD%D0%BE%D0%B4%D1%8B)
* [Становимся валидатором](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D0%BC%D1%81%D1%8F-%D0%B2%D0%B0%D0%BB%D0%B8%D0%B4%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%BC)
* [Установка стейкинг пула](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-%D1%81%D1%82%D0%B5%D0%B9%D0%BA%D0%B8%D0%BD%D0%B3-%D0%BF%D1%83%D0%BB%D0%B0)
* [Инструкция по транзакциям](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%86%D0%B8%D1%8F-%D0%BF%D0%BE-%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D1%8F%D0%BC)
* [Пинг](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%BF%D0%B8%D0%BD%D0%B3)
* [Мониторинг](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%BC%D0%BE%D0%BD%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%BD%D0%B3)
* [Подключение мониторинга](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BC%D0%BE%D0%BD%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%BD%D0%B3%D0%B0)

Покупка VPS
===
В первую очередь нужно определиться с сервером, на котором будем разворачивать ноду NEAR. Мы решили остановиться на HETZNER, т.к. у провайдера демократичные цены и высокая надежность.

* Переходим к списку серверов и их техническим характеристикам:
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/1.png)
> **Минимальные требования для запуска ноды NEAR следующие:**
> - CPU 4-ядерный процессор с поддержкой
> - AVX RAM 8GB DDR4
> - STORAGE 500GB SSD

Соответственно выбираем тот сервер, который равен по характеристикам или превосходит их. В нашем случае это был сервер **AX101**.

* Перемещаемся к окну конфигурации сервера, где выбираем его локацию, операционную систему, уточняем характеристики и цену. Убедившись, что всё на месте, переходим к покупке сервера, нажав на кнопку **ORDER NOW**:

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/2.png)     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/3.png)
---|---

Сохраняем заказ:     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/4.png)
:---:|---
**Далее его необходимо подтвердить:**     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/5.png)
**Следующим шагом нам откроется страница регистрации учетной записи, регистрируемся и выбираем удобный вид оплаты сервера:**     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/6.png)
**После покупки, нам придет письмо на почтовый ящик:**     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/7.jpg)

#### На этом оформление и покупка сервера для NEAR завершена.
***
Создание кошелька
===
В первую очередь нам нужно создать кошелек по этому адресу — <https://wallet.shardnet.near.org/>

Для этого проделываем следующие шаги:
 Шаги | Скриншоты 
----------------|----------------------
1️⃣ Нажимаем на кнопку “**Создать учетную запись**”:       | ![Создание учетой записи](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.1%20-%20wallet.png)
2️⃣ Указываем **имя** для учетной записи:       | ![Имя учетной записи](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.2%20-%20wallet.png)
3️⃣ Выбор метода восстановления учетной записи, рекомендуем использовать **мнемоническую фразу**:   | ![Выбор метода восстановления](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.3%20-%20wallet.png)
4️⃣ Записываем мнемоническую фразу в надежное место       | ![Мнемоническая фраза](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.4.1%20-%20wallet.png)
5️⃣ Проходим проверку:    | ![Проверка](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.5.1%20-%20wallet.png)
6️⃣ Получаем доступ к учетной записи:    | ![Доступ к учетной записи](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.6%20-%20wallet.png)

Установка NEAR-CLI
===
* Для начала, давайте убедимся, что машина Linux обновлена:
```
sudo apt update && sudo apt upgrade -y
```
***
* Далее установим `Node.js` и `npm`:
```
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y build-essential nodejs
PATH="$PATH"
```
***
* Проверяем версию `Node.js` и `npm`:
```
node -v
```
>⚠️ **Требуемая версия _v18.x.x_ или выше**


```
npm -v
```
>⚠️ **Требуемая версия _v8.x.x_ или выше**
***
* Переходим к непосредственной установке NEAR-CLI:
```
sudo npm install -g near-cli
```
***
* Т.к. этот гайд предназначен для сети **shardnet**, пишем команды:
```
export NEAR_ENV=shardnet
```

```
echo 'export NEAR_ENV=shardnet' >> ~/.bashrc
echo 'export NEAR_ENV=shardnet' >> ~/.bash_profile 
source $HOME/.bash_profile
```
***
После завершения, мы сможем пользоваться базовыми командами **NEAR-CLI**, такими как:
Команда   | Результат
:---:|:---:
`near proposals`: показывает предложение валидаторов     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.8%20-%20proposals.png)
`near validators current`: показывает валидаторов в текущей эпохе     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.7%20-%20current.png)
`near validators next`: показывает валидаторов, которые станут валидировать в следующей эпохе     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.9%20-%20next.png)
***

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

Установка стейкинг пула
===
Стейкинг пул — это смарт-контракт, развернутый на учетной записи NEAR. Вызов команды стейкинг пула, создает пул с указанным именем и развертывает его на указанный `accountId`.

Пример команды:
```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "<pool id>", "owner_id": "<accountId>", "stake_public_key": "<public key>", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"5if1dPtovQ9pMd1CacZVmBHhU13szy7jKoZyKYkGdeba"}' --accountId="<accountId>" --amount=30 --gas=300000000000000
```

Из примера выше следует, что вам нужно заменить:
* `pool id`: имя стейкинг пула, слово “factory” автоматически добавится к этому параметру, создавая {pool_id}.{staking_pool_factory} 
Пример: если Pool ID “btcsecure”, то будет : `btcsecure.factory.shardnet.near`
* `owner_id`: это аккаунт в SHARDNET (`btcsecure.shardnet.near`), который будет управлять стейкинг пулом
* `public key`: публичный ключ, расположенный в файле `validator_key.json`
* `5`: комиссия пула, где 5 — это 5%
* `accountId`: SHARDNET аккаунт, разворачивающий и подписывающий транзакции. Обычно `accountId` = `owner_id`

> *Убеждаемся, что на аккаунте есть 30 NEAR — это минимум, необходимый для хранения.*

* Наша команда для запуска пула:
```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "btcsecure.factory.shardnet.near", "owner_id": "<accountId>", "stake_public_key": " ed25519:AbskEuvTEx9GvGz9CFLdqfPzgHiSVnJ2C6QwoPyExFYo", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="btcsecure.shardnet.near" --amount=30 --gas=300000000000000
```

### ✅Стейкинг пул успешно [создан](https://explorer.shardnet.near.org/transactions/FNdHdSa98osh3VdbK3aEX71N6ofsmb8skoko7BriPRc4)!
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-003/19.1.png)
***
Чтобы изменить параметры пула, например, изменить размер взимаемой комиссии на 1%, используем эту команду:
```
near call <pool_name> update_reward_fee_fraction '{"reward_fee_fraction": {"numerator": 1, "denominator": 100}}' --accountId <account_id> --gas=300000000000000
```
Пример:
```
near call btcsecure.factory.shardnet.near update_reward_fee_fraction '{"reward_fee_fraction": {"numerator": 1, "denominator": 100}}' --accountId btcsecure.shardnet.near --gas=300000000000000
```

#### Теперь мы, наконец, настроили наш стейкинг пул
Проверить появился ли пул в списке можно по этой [ссылке](https://explorer.shardnet.near.org/nodes/validators).

Инструкция по транзакциям
===
* Депозит и стейкинг NEAR:
```
near call <staking_pool_id> deposit_and_stake --amount <amount> --accountId <accountId> --gas=300000000000000
```

* Анстейк NEAR:
```
near call <staking_pool_id> unstake '{"amount": "<amount yoctoNEAR>"}' --accountId <accountId> --gas=300000000000000
```

* Чтобы анстейкнуть всё, используейте эту команду:
```
near call <staking_pool_id> unstake_all --accountId <accountId> --gas=300000000000000
```

* Вывести средства:
```
near call <staking_pool_id> withdraw '{"amount": "<amount yoctoNEAR>"}' --accountId <accountId> --gas=300000000000000
```

* Команда, чтобы вывести всё:
```
near call <staking_pool_id> withdraw_all --accountId <accountId> --gas=300000000000000
```

### Мы можем видеть наши вызовы смарт-контрактов в [эксплорере](https://explorer.shardnet.near.org/accounts/btcsecure.shardnet.near)
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-003/22.png)

Пинг
===
Пинг выдает новое предложение и обновляет баланс ставок для ваших делегатов. Для поддержания актуальности сообщений о вознаграждениях следует проводить пинг каждую эпоху.

* Команда:
```
near call <staking_pool_id> ping '{}' --accountId <accountId> --gas=300000000000000
```

* Команда, чтобы узнать общий баланс:
```
near view <staking_pool_id> get_account_total_balance '{"account_id": "<accountId>"}'
```

* Стейкинг баланса:
```
near view <staking_pool_id> get_account_staked_balance '{"account_id": "<accountId>"}'
```

* Анстейкнутый баланс:
```
near view <staking_pool_id> get_account_unstaked_balance '{"account_id": "<accountId>"}'
```

* Доступно для вывода средств:
```
near view <staking_pool_id> is_account_unstaked_balance_available '{"account_id": "<accountId>"}'
```

* Пауза стейкинга:
```
near call <staking_pool_id> pause_staking '{}' --accountId <accountId>
```

* Возобновление стейкинга:
```
near call <staking_pool_id> resume_staking '{}' --accountId <accountId>
```
***

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
Вернуться к оглавлению(# Пошаговая инструкция по запуску валидатора в сети ShardNet
* [Покупка VPS](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%BF%D0%BE%D0%BA%D1%83%D0%BF%D0%BA%D0%B0-vps)
* [Создание кошелька](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BA%D0%BE%D1%88%D0%B5%D0%BB%D1%8C%D0%BA%D0%B0)
* [Установка NEAR-CLI](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-near-cli)
* [Настройка ноды](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%BD%D0%BE%D0%B4%D1%8B)
* [Становимся валидатором](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D0%BC%D1%81%D1%8F-%D0%B2%D0%B0%D0%BB%D0%B8%D0%B4%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%BC)
* [Установка стейкинг пула](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-%D1%81%D1%82%D0%B5%D0%B9%D0%BA%D0%B8%D0%BD%D0%B3-%D0%BF%D1%83%D0%BB%D0%B0)
* [Инструкция по транзакциям](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%86%D0%B8%D1%8F-%D0%BF%D0%BE-%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D1%8F%D0%BC)
* [Пинг](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%BF%D0%B8%D0%BD%D0%B3)
* [Мониторинг](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%BC%D0%BE%D0%BD%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%BD%D0%B3)
* [Подключение мониторинга](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BC%D0%BE%D0%BD%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%BD%D0%B3%D0%B0)

Покупка VPS
===
В первую очередь нужно определиться с сервером, на котором будем разворачивать ноду NEAR. Мы решили остановиться на HETZNER, т.к. у провайдера демократичные цены и высокая надежность.

* Переходим к списку серверов и их техническим характеристикам:
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/1.png)
> **Минимальные требования для запуска ноды NEAR следующие:**
> - CPU 4-ядерный процессор с поддержкой
> - AVX RAM 8GB DDR4
> - STORAGE 500GB SSD

Соответственно выбираем тот сервер, который равен по характеристикам или превосходит их. В нашем случае это был сервер **AX101**.

* Перемещаемся к окну конфигурации сервера, где выбираем его локацию, операционную систему, уточняем характеристики и цену. Убедившись, что всё на месте, переходим к покупке сервера, нажав на кнопку **ORDER NOW**:

![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/2.png)     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/3.png)
---|---

Сохраняем заказ:     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/4.png)
:---:|---
**Далее его необходимо подтвердить:**     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/5.png)
**Следующим шагом нам откроется страница регистрации учетной записи, регистрируемся и выбираем удобный вид оплаты сервера:**     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/6.png)
**После покупки, нам придет письмо на почтовый ящик:**     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-005/7.jpg)

#### На этом оформление и покупка сервера для NEAR завершена.
***
Создание кошелька
===
В первую очередь нам нужно создать кошелек по этому адресу — <https://wallet.shardnet.near.org/>

Для этого проделываем следующие шаги:
 Шаги | Скриншоты 
----------------|----------------------
1️⃣ Нажимаем на кнопку “**Создать учетную запись**”:       | ![Создание учетой записи](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.1%20-%20wallet.png)
2️⃣ Указываем **имя** для учетной записи:       | ![Имя учетной записи](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.2%20-%20wallet.png)
3️⃣ Выбор метода восстановления учетной записи, рекомендуем использовать **мнемоническую фразу**:   | ![Выбор метода восстановления](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.3%20-%20wallet.png)
4️⃣ Записываем мнемоническую фразу в надежное место       | ![Мнемоническая фраза](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.4.1%20-%20wallet.png)
5️⃣ Проходим проверку:    | ![Проверка](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.5.1%20-%20wallet.png)
6️⃣ Получаем доступ к учетной записи:    | ![Доступ к учетной записи](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.6%20-%20wallet.png)

Установка NEAR-CLI
===
* Для начала, давайте убедимся, что машина Linux обновлена:
```
sudo apt update && sudo apt upgrade -y
```
***
* Далее установим `Node.js` и `npm`:
```
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y build-essential nodejs
PATH="$PATH"
```
***
* Проверяем версию `Node.js` и `npm`:
```
node -v
```
>⚠️ **Требуемая версия _v18.x.x_ или выше**


```
npm -v
```
>⚠️ **Требуемая версия _v8.x.x_ или выше**
***
* Переходим к непосредственной установке NEAR-CLI:
```
sudo npm install -g near-cli
```
***
* Т.к. этот гайд предназначен для сети **shardnet**, пишем команды:
```
export NEAR_ENV=shardnet
```

```
echo 'export NEAR_ENV=shardnet' >> ~/.bashrc
echo 'export NEAR_ENV=shardnet' >> ~/.bash_profile 
source $HOME/.bash_profile
```
***
После завершения, мы сможем пользоваться базовыми командами **NEAR-CLI**, такими как:
Команда   | Результат
:---:|:---:
`near proposals`: показывает предложение валидаторов     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.8%20-%20proposals.png)
`near validators current`: показывает валидаторов в текущей эпохе     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.7%20-%20current.png)
`near validators next`: показывает валидаторов, которые станут валидировать в следующей эпохе     | ![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-001/0.9%20-%20next.png)
***

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

Установка стейкинг пула
===
Стейкинг пул — это смарт-контракт, развернутый на учетной записи NEAR. Вызов команды стейкинг пула, создает пул с указанным именем и развертывает его на указанный `accountId`.

Пример команды:
```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "<pool id>", "owner_id": "<accountId>", "stake_public_key": "<public key>", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"5if1dPtovQ9pMd1CacZVmBHhU13szy7jKoZyKYkGdeba"}' --accountId="<accountId>" --amount=30 --gas=300000000000000
```

Из примера выше следует, что вам нужно заменить:
* `pool id`: имя стейкинг пула, слово “factory” автоматически добавится к этому параметру, создавая {pool_id}.{staking_pool_factory} 
Пример: если Pool ID “btcsecure”, то будет : `btcsecure.factory.shardnet.near`
* `owner_id`: это аккаунт в SHARDNET (`btcsecure.shardnet.near`), который будет управлять стейкинг пулом
* `public key`: публичный ключ, расположенный в файле `validator_key.json`
* `5`: комиссия пула, где 5 — это 5%
* `accountId`: SHARDNET аккаунт, разворачивающий и подписывающий транзакции. Обычно `accountId` = `owner_id`

> *Убеждаемся, что на аккаунте есть 30 NEAR — это минимум, необходимый для хранения.*

* Наша команда для запуска пула:
```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "btcsecure.factory.shardnet.near", "owner_id": "<accountId>", "stake_public_key": " ed25519:AbskEuvTEx9GvGz9CFLdqfPzgHiSVnJ2C6QwoPyExFYo", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="btcsecure.shardnet.near" --amount=30 --gas=300000000000000
```

### ✅Стейкинг пул успешно [создан](https://explorer.shardnet.near.org/transactions/FNdHdSa98osh3VdbK3aEX71N6ofsmb8skoko7BriPRc4)!
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-003/19.1.png)
***
Чтобы изменить параметры пула, например, изменить размер взимаемой комиссии на 1%, используем эту команду:
```
near call <pool_name> update_reward_fee_fraction '{"reward_fee_fraction": {"numerator": 1, "denominator": 100}}' --accountId <account_id> --gas=300000000000000
```
Пример:
```
near call btcsecure.factory.shardnet.near update_reward_fee_fraction '{"reward_fee_fraction": {"numerator": 1, "denominator": 100}}' --accountId btcsecure.shardnet.near --gas=300000000000000
```

#### Теперь мы, наконец, настроили наш стейкинг пул
Проверить появился ли пул в списке можно по этой [ссылке](https://explorer.shardnet.near.org/nodes/validators).

Инструкция по транзакциям
===
* Депозит и стейкинг NEAR:
```
near call <staking_pool_id> deposit_and_stake --amount <amount> --accountId <accountId> --gas=300000000000000
```

* Анстейк NEAR:
```
near call <staking_pool_id> unstake '{"amount": "<amount yoctoNEAR>"}' --accountId <accountId> --gas=300000000000000
```

* Чтобы анстейкнуть всё, используейте эту команду:
```
near call <staking_pool_id> unstake_all --accountId <accountId> --gas=300000000000000
```

* Вывести средства:
```
near call <staking_pool_id> withdraw '{"amount": "<amount yoctoNEAR>"}' --accountId <accountId> --gas=300000000000000
```

* Команда, чтобы вывести всё:
```
near call <staking_pool_id> withdraw_all --accountId <accountId> --gas=300000000000000
```

### Мы можем видеть наши вызовы смарт-контрактов в [эксплорере](https://explorer.shardnet.near.org/accounts/btcsecure.shardnet.near)
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-003/22.png)

Пинг
===
Пинг выдает новое предложение и обновляет баланс ставок для ваших делегатов. Для поддержания актуальности сообщений о вознаграждениях следует проводить пинг каждую эпоху.

* Команда:
```
near call <staking_pool_id> ping '{}' --accountId <accountId> --gas=300000000000000
```

* Команда, чтобы узнать общий баланс:
```
near view <staking_pool_id> get_account_total_balance '{"account_id": "<accountId>"}'
```

* Стейкинг баланса:
```
near view <staking_pool_id> get_account_staked_balance '{"account_id": "<accountId>"}'
```

* Анстейкнутый баланс:
```
near view <staking_pool_id> get_account_unstaked_balance '{"account_id": "<accountId>"}'
```

* Доступно для вывода средств:
```
near view <staking_pool_id> is_account_unstaked_balance_available '{"account_id": "<accountId>"}'
```

* Пауза стейкинга:
```
near call <staking_pool_id> pause_staking '{}' --accountId <accountId>
```

* Возобновление стейкинга:
```
near call <staking_pool_id> resume_staking '{}' --accountId <accountId>
```
***

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
### ⏫[Вернуться к оглавлению](https://github.com/BTCSecure/stakewars-3/blob/main/guide.md#%D0%BF%D0%BE%D1%88%D0%B0%D0%B3%D0%BE%D0%B2%D0%B0%D1%8F-%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%86%D0%B8%D1%8F-%D0%BF%D0%BE-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D1%83-%D0%B2%D0%B0%D0%BB%D0%B8%D0%B4%D0%B0%D1%82%D0%BE%D1%80%D0%B0-%D0%B2-%D1%81%D0%B5%D1%82%D0%B8-shardnet)
