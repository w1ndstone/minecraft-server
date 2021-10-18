# Подробный гайд по созданию и настройке сервера Minecraft

## Хостинг

### 



### Собственный компьютер в качестве хоста

Если Вы хотите использовать собственный ПК в качестве хоста сервера, то Вам понадобится:

* Запустить сервер;
* Пробросить порты.

Для проброса портов необходим **белый IP**, желательно статический (для удобства), а также, чтобы провайдер не блокировал порты. Пробросить порты по протоколу TCP можно через настройки роутера, брандмауэр и даже торрент-клиент.

**Но что делать, если у Вас серый айпи/провайдер блокирует порты?**

Здесь есть два варианта - воспользоваться Ngrok или VPN (OpenVPN, HideMyName)

С помощью ngrok: заходим на [данный сайт](https://ngrok.com/), регистрируемся и скачиваем программу, после чего заходим в личный кабинет, копируем authtoken, открываем сам ngrok и вставляем туда токен:

`ngrok authtoken ваш токен`

после чего вписываем

`ngrok tcp -region eu 25565`

и получаем наш айпи, по которому можно подключиться к серверу. (такого вида: 0.tcp.eu.ngrok.io:12345)

С помощью VPN:



### Буквенный IP

Для этого Вам нужно получить свой домен, после чего на [cloudflare](https://www.cloudflare.com/ru-ru/) создать SRV запись.

## Java

Рекомендуемые:

* [AdoptOpenJDK](https://adoptopenjdk.net/installation.html?variant=openjdk16&jvmVariant=hotspot)
* [ZuluJDK](https://www.azul.com/downloads/?package=jdk)
* [AmazonJDK](https://aws.amazon.com/ru/corretto/)

## Выбор ядра сервера

* [Airplane](https://github.com/Technove/Airplane) - на сегодняшний день является одним из лучших в плане производительности и стабильности. Основано на Paper.
* [Purpur](https://github.com/pl3xgaming/Purpur) - обеспечивает высокую производительность, имеет большое количество геймплейных изменений, удобную конфигурацию. Основано на Airplane.
* [Paper](https://github.com/PaperMC/Paper) - одно из самых популярных ядер в Minecraft, обеспечивающее хорошую производительность.
* [Spigot](https://getbukkit.org/download/spigot) - форк CraftBukkit с улучшенной производительностью. На сегодняшний день сильно уступает другим ядрам по производительности.
* [CraftBukkit](https://getbukkit.org/download/craftbukkit) - ванильное ядро с возможностью ставить плагины. На сегодняшний день сильно уступает другим ядрам по производительности.
* [Yatopia](https://github.com/YatopiaMC/Yatopia) - форк огромного количества ядер. Крайне нестабильное ядро, не рекомендую использованию.
* [Sugarcane](https://github.com/SugarcaneMC/Sugarcane) - форк Paper, Tuinity, Airplane, Purpur и Yatopia. Не рекомендую к использованию.
* [Patina](https://github.com/PatinaMC/Patina) - форк Yatopia. Не рекомендую к использованию.

## Пре-генерация чанков

Предварительная генерация чанков - один из важнейших шагов в улучшении производительности сервера. Во время перемещения по миру постоянно генерируются новые чанки, которые создают существенную нагрузку на сервер, и обычно на слабых ПК это влечет за собой низкий тпс и очень медленную прогрузку чанков.

Предварительно прогрузить чанки можно следующим плагином:

* [Chunky](https://www.spigotmc.org/resources/chunky.81534/)

## Конфигурация файлов

### server.properties

`network-compression-threshold`

Данная опция ограничивает размер пакета до того, как сервер попытается его сжать. Установка более высокого значения может сэкономить некоторые ресурсы процессора, а установка значения `-1` отключает его. Не рекомендуется ставить значение ниже `64`и выше `1500.`

> Оптимальным значением является `512`. Если ваш сервер является локальным, отключение этого параметра (-1) будет полезным.

### bukkit.yml

#### spawn-limits

```
Good starting values:

    monsters: 20
    animals: 5
    water-animals: 2
    water-ambient: 2
    ambient: 1
```

The math of limiting mobs is `[playercount] * [limit]`, where "playercount" is current amount of players on the server. Logically, the smaller the numbers are, the less mobs you're gonna see. `per-player-mob-spawn` applies an additional limit to this, ensuring mobs are equally distributed between players. Reducing this is a double-edged sword; yes, your server has less work to do, but in some gamemodes natural-spawning mobs are a big part of a gameplay. You can go as low as 20 or less if you adjust `mob-spawn-range` properly. Setting `mob-spawn-range` lower will make it feel as if there are more mobs around each player. If you are using Paper, you can set mob limits per world in [`paper.yml`].



### spigot.yml

`view-distance`

Это расстояние в чанках вокруг игрока, в которых может что-либо происходить. Это включает в себя плавку в печах, выращивание сельскохозяйственных культур и саженцев и т. Д. Вы должны установить это значение именно в `spigot.yml`, так как оно заменяет значение из `server.properties` и может быть установлено для каждого мира. Это вариант, который вы хотите намеренно установить на низком уровне, где-то около «3» или «4», из-за существования «no-tick-view-distance». Без отметки позволяет игрокам загружать больше кусков, не отмечая их. Это эффективно позволяет игрокам видеть дальше без того же снижения производительности.

> Оптимальным значением является `4`.

### paper.yml

`anti-xray`

. For detailed configuration of this feature check out [Stonar96's recommended settings](https://gist.github.com/stonar96/ba18568bd91e5afd590e8038d14e245e). Включение данной опции будет снижать производительность сервера, однако, оно все же эффективнее плагинов на anti-xray. В большинстве случаях влияние на производительность незначительная.

> Оптимальным значением является `true`.

### tuinity.yml



### airplane.air



### purpur.yml

#### use-alternate-keepalive

`Good starting value: true`

You can enable Purpur's alternate keepalive system so players with bad connection don't get timed out as often. Has known incompatibility with TCPShield.

> Enabling this sends a keepalive packet once per second to a player, and only kicks for timeout if none of them were responded to in 30 seconds. Responding to any of them in any order will keep the player connected. AKA, it won't kick your players because 1 packet gets dropped somewhere along the lines  
~ https://purpur.pl3x.net/docs/Configuration/#use-alternate-keepalive

-------------------------------------------------

Your garbage collector can be configured to reduce lag spikes caused by big garbage collector tasks. You can find startup flags optimized for Minecraft servers [here](https://mcflags.emc.gs/) [`SOG`]. Keep in mind that this recommendation will not work on alternative jvm implementations.

# Linux CPU scaling 
Some hosts might ship machines running in "PowerSave" mode. This can result in nearly 25% lower clock speeds and thus vastly lower single threaded performance. This can lead to severly worse performance than setting the CPU scaling to performance mode. Please note that this might be unavailable for VPS.

For Debian / Ubuntu

`cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor` Shows the CPU's performance profile.

`echo "performance" | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor` Sets profile to performance.

# "Too good to be true" plugins

## Plugins removing ground items
Absolutely unnecessary since they can be replaced with [merge radius](#merge-radius) and [alt-item-despawn-rate](#alt-item-despawn-rate) and frankly, they're less configurable than basic server configs. They tend to use more resources scanning and removing items than not removing the items at all.

## Mob stacker plugins
It's really hard to justify using one. Stacking naturally spawned entities causes more lag than not stacking them at all due to the server constantly trying to spawn more mobs. The only "acceptable" use case is for spawners on servers with a large amount of spawners.

## Plugins enabling/disabling other plugins
Anything that enables or disables plugins on runtime is extremely dangerous. Loading a plugin like that can cause fatal errors with tracking data and disabling a plugin can lead to errors due to removing dependency. The `/reload` command suffers from exact same issues and you can read more about them in [me4502's blog post](https://madelinemiller.dev/blog/problem-with-reload/)

# What's lagging? - measuring performance

## mspt
Paper offers a `/mspt` command that will tell you how much time the server took to calculate recent ticks. If the first and second value you see are lower than 50, then congratulations! Your server is not lagging! If the third value is over 50 then it means there was at least 1 tick that took longer. That's completely normal and happens from time to time, so don't panic.

## timings
Great way to see what might be going on when your server is lagging are timings. Timings is a tool that lets you see exactly what tasks are taking the longest. It's the most basic troubleshooting tool and if you ask for help regarding lag you will most likely be asked for your timings.

To get timings of your server you just need to execute the `/timings paste` command and click the link you're provided with. You can share this link with other people to let them help you. It's also easy to misread if you don't know what you're doing. There is a detailed [video tutorial by Aikar](https://www.youtube.com/watch?v=T4J0A9l7bfQ) on how to read them.
  
## spark
[Spark](https://github.com/lucko/spark) is a plugin that allows you to profile your servers CPU and memory usage. You can read on how to use it [on its wiki](https://spark.lucko.me/docs/). There's also a guide on how to find the cause of lag spikes [here](https://spark.lucko.me/docs/guides/Finding-lag-spikes).


[`SOG`]: https://www.spigotmc.org/threads/guide-server-optimization%E2%9A%A1.283181/
[server.properties]: https://minecraft.fandom.com/Server.properties
[bukkit.yml]: https://bukkit.gamepedia.com/Bukkit.yml
[spigot.yml]: https://www.spigotmc.org/wiki/spigot-configuration/
[paper.yml]:  https://paper.readthedocs.io/en/latest/server/configuration.html
[purpur.yml]: https://purpur.pl3x.net/docs
[airplane.yml]: https://github.com/TECHNOVE/Airplane/wiki
