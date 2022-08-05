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

* При установке увидим следующее:
