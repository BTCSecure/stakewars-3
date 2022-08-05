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

Выбор выделенного сервера
===
Далее необходимо развернуть **NEAR-CLI** на сервере, который мы приобрели в Challenge 005.

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
* `near proposals`: показывает предложение валидаторов;
* `near validators current`: показывает валидаторов в текущей эпохе;
* `near validators next`: показывает валидаторов, которые станут валидировать в следующей эпохе.
***
⏩Перейти к [Challenge 002](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-002.md)
