# Мониторинг аптайма
### Открываем порт 3030 для диагностических отчетов

* Проверяем открыт ли порт 3030:

```
sudo iptables -L | grep 3030
```

* Открываем порт, если он закрыт:

```
sudo iptables -A INPUT -p tcp --dport 3030 -j ACCEPT
```

* Сохраняем конфиг и для этого есть два решения:

### Использование `iptables-persistent`:
* Команда

```
sudo apt install iptables-persistent
```

* Или если он уже установлен

```
sudo dpkg-reconfigure iptables-persistent
```

### Использование файлов:
```
iptables-save > /etc/iptables/rules.v4
ip6tables-save > /etc/iptables/rules.v6
```

### Убедимся, что порт открыт, посетив адрес:
[http://<NODE_IP>:3030/status](http://<NODE_IP>:3030/status)
> Где **<NODE_IP>** — это IP адрес ноды.
> 
> *В некоторых случаях порт также может потребоваться открыть у провайдера или в файерволле датацентра*

#### Адрес ноды btcsecure:
 <http://65.109.22.107:3030/status>

Место в лидерборде <https://openshards.io/shardnet-uptime-scoreboard/>
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-009/21-Leaderboard.png)
***
⏪[Challenge 008](https://github.com/BTCSecure/stakewars-3/blob/main/challenge-008.md)     | [Оглавление](https://github.com/BTCSecure/stakewars-3#%D0%BF%D0%BE%D1%88%D0%B0%D0%B3%D0%BE%D0%B2%D0%B0%D1%8F-%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%86%D0%B8%D1%8F-%D0%BF%D0%BE-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D1%83-%D0%B2%D0%B0%D0%BB%D0%B8%D0%B4%D0%B0%D1%82%D0%BE%D1%80%D0%B0)⏩
:---|---:
