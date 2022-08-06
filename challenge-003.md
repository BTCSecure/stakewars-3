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
⏪[Challenge 002](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-002.md)     | [Challenge 004](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-004.md)⏩
---|---:
