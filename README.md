# Гайд по созданию и настройке сервера Minecraft

## Содержание

* Хостинг

    * Бесплатные хостинги
    * Платные хостинги
    * Собственный компьютер в качестве хоста

* Доменный адрес

* Java

    * Java аргументы запуска

* Выбор ядра сервера

* Пре-генерация чанков

* Конфигурация файлов

    * server.properties
    * bukkit.yml
    * spigot.yml
    * paper.yml
    * tuinity.yml
    * airplane.air
    * purpur.yml

* Оптимизация операционной системы

    * Linux
    * Windows

## Хостинг

### Бесплатные хостинги

* [Heroku](https://heroku.com)

подробный [гайд](https://www.youtube.com/watch?v=EBzkSDBmaoU&t=130s) по запуску сервера на данном хостинге.

* [Aternos](https://aternos.org/:ru/)
* [Minehut](https://minehut.com/)

### Платные хостинги

* [Hostinger](https://www.hostinger.ru/vps-hosting-servera)
* [RUVDS](https://ruvds.com/ru-rub)

### Собственный компьютер в качестве хоста

Если Вы хотите использовать собственный ПК в качестве хоста сервера, то Вам понадобится:

* Запустить сервер;
* Пробросить порты.

Для проброса портов необходим **белый IP**, а также, чтобы провайдер не блокировал порты. Пробросить порты по протоколу TCP можно через настройки роутера, брандмауэр и даже торрент-клиент.

**Но что делать, если у Вас серый айпи/провайдер блокирует порты?**

Здесь есть три варианта - воспользоваться [Ngrok](https://ngrok.com/), VPN (OpenVPN, HideMyName) или [IPv6](http://rubukkit.org/threads/ipv6-shag-v-buduschee-ili-obxodim-seryj-ip-bez-hamachi.35342/).

## Доменный адрес

Для этого Вам нужно получить свой домен, после чего на [cloudflare](https://www.cloudflare.com/ru-ru/) настроить SRV запись.

## Java

Рекомендуемые:

* [AdoptOpenJDK](https://adoptopenjdk.net/installation.html?variant=openjdk16&jvmVariant=hotspot)
* [ZuluJDK](https://www.azul.com/downloads/?package=jdk)
* [AmazonJDK](https://aws.amazon.com/ru/corretto/)

### Java аргументы запуска

[Оптимизация JVM аргументов запуска](https://mcflags.emc.gs/)

## Выбор ядра сервера

Рекомендуемые ядра:
* [Airplane](https://github.com/Technove/Airplane) - на сегодняшний день является одним из лучших в плане производительности и стабильности. Основано на Paper.
* [Purpur](https://github.com/pl3xgaming/Purpur) - обеспечивает высокую производительность, имеет большое количество геймплейных изменений, удобную конфигурацию. Основано на Airplane.
* [Paper](https://github.com/PaperMC/Paper) - одно из самых популярных ядер в Minecraft, обеспечивающее неплохую производительность.

Ядра, которые нужно обходить стороной:
* [Spigot](https://getbukkit.org/download/spigot) - форк CraftBukkit с улучшенной производительностью. На сегодняшний день уступает другим ядрам по производительности.
* [CraftBukkit](https://getbukkit.org/download/craftbukkit) - ванильное ядро с возможностью ставить плагины. На сегодняшний день сильно уступает другим ядрам по производительности.
* [Yatopia](https://github.com/YatopiaMC/Yatopia) - форк огромного количества ядер. Крайне нестабильное ядро.
* [Sugarcane](https://github.com/SugarcaneMC/Sugarcane) - форк Paper, Tuinity, Airplane, Purpur и Yatopia.
* [Patina](https://github.com/PatinaMC/Patina) - форк Yatopia.
* [Mohist]() - нестабильное ядро.
* [MCPC+]() - нестабильное ядро.

## Пре-генерация чанков

Предварительная генерация чанков - один из важнейших шагов в улучшении производительности сервера. Во время перемещения по миру постоянно генерируются новые чанки, которые создают существенную нагрузку на сервер, и обычно на слабых ПК это влечет за собой низкий тпс и очень медленную прогрузку чанков.

Предварительно прогрузить чанки можно следующим плагином:

* [Chunky](https://www.spigotmc.org/resources/chunky.81534/)

## Конфигурация файлов

### [server.properties](https://minecraft.fandom.com/Server.properties)

#### `network-compression-threshold`

Ограничивает размер пакета до того, как сервер попытается его сжать. Установка более высокого значения может сэкономить некоторые ресурсы процессора, а установка значения `-1` отключает его. Не рекомендуется ставить значение ниже `64`и выше `1500`.

> Оптимальным значением является `512`. Если ваш сервер является локальным, отключение этого параметра будет полезным.

### [bukkit.yml](https://bukkit.gamepedia.com/Bukkit.yml)

#### `allow-end`

Определяет, будет ли включено измерение края. 

> Если Вам данное измерение не нужно, можете смело ставить `false`.

#### `spawn-limits`

Ограничивает количество мобов на всём сервере.

> Оптимальными значениями являются 

> monsters: `50`

> animals: `8`

> water-animals: `3`

> water-ambient: `10`

> ambient: `1`.

#### `ticks-per`

Определяет, раз в сколько тиков сервер будет пытаться заспавнить моба.

> Оптимальными значениями являются

> monster-spawn: `4`

> animal-spawns: `400`

> water-spawns: `400`

> water-ambient-spawns: `400`

> water-underground-creature-spawns: `400`

> ambient-spawns: `400`.

### [spigot.yml](https://www.spigotmc.org/wiki/spigot-configuration/)

#### `view-distance`

Это расстояние в чанках вокруг игрока, в котором может что-либо происходить. Это включает в себя плавку в печах, выращивание саженцев. Вы должны установить это значение именно в `spigot.yml`, так как оно заменяет значение из `server.properties` и может быть установлено для каждого мира.

> Оптимальным значением является `4`.

#### `ticks-per`

Определяет за сколько тиков воронка может передать предмет.

> Оптимальными значениями являются

> hopper-transfer: `8`

> hopper-check: `8`.

#### `mob-spawn-range`

Ограничивает диапазон появления мобов вокруг игрока.

> Оптимальным значением яляется `2`.

#### `entity-activation-range`

Дистанция обнаружения игрока. Уменьшение данных значений увеличивает производительность, но может сломать фермы мобов.

> Оптимальными значениями являются

> animals: `16`

> monsters: `24`

> raiders: `48`

> misc: `8`

> water: `8`

> villagers: `16`

> flying-monsters: `48`.

#### `entity-tracking-range`

Дистанция видимости мобов. Не занижайте слишком сильно.

> Оптимальными значениями являются

> players: `48`

> animals: `48`

> monsters: `48`
      
> misc: `32`

> other: `64`.

#### `tick-inactive-villagers`

Отключение этого параметра улучшает производительность, но в определенных ситуациях может сбивать с толку игроков. Это может вызвать проблемы с фермами железа.

> Оптимальным значением является `false`.

#### `nerf-spawner-mobs`

Отвечает за ИИ мобов, появившихся из спавнеров. При включении данного параметра они ничего не будут делать. В воде они смогут плавать только когда будет включен параметр `spawner-nerfed-mobs-should-jump` в [paper.yml](https://paper.readthedocs.io/en/latest/server/configuration.html).

> Оптимальным значением является `true`.

#### `merge-radius`

Определяет дистанцию между одинаковыми предметами и сферами опыта, при пересечении которой они объединятся. Слишком высокое значение увеличит производительность, но вохможно сломает фермы.

> Оптимальными значениями являются

> item: `3.5`

> exp: `4.0`.

### [paper.yml](https://paper.readthedocs.io/en/latest/server/configuration.html)

#### `no-tick-view-distance`

Данный параметр определяет расстояние в чанках вокруг игрока, которое будет прогружаться, но в котором ничего не будет происходить.

> Оптимальным значением является `12`.

#### `delay-chunk-unloads-by`

Определяет, через сколько выгрузится чанк, если в нем отсутствуют игроки.

> Оптимальным значением является `10`.

#### `max-auto-save-chunks-per-tick`

> Оптимальным значением является `8`.

#### `prevent-moving-into-unloaded-chunks`

> Оптимальным значением является `true`.

#### `entity-per-chunk-save-limit`

> Оптимальными значениями являются

> experience_orb: `16`

> arrow: `16`

> dragon_fireball: `3`

> egg: `8`

> ender_pearl: 8

> eye_of_ender: 8

> fireball: `8`

> small_fireball: `8`

> firework_rocket: `8`

> potion: `8`

> llama_spit: `3`

> shulker_bullet: `8`

> snowball: `8`

> spectral_arrow: `16`

> experience_bottle: `3`

> trident: `16`

> wither_skull: `4`

> area_effect_cloud: `8`.

#### `seed-based-feature-search-loads-chunks`

> Оптимальным значением являются `true`.

#### `despawn-ranges`

> Оптимальным значениями являются

> soft: `30`
> hard: `56`.

#### `per-player-mob-spawns`

> Оптимальным значением является `true`.

#### `max-entity-collisions`

> Оптимальным значением является `2`.

#### `update-pathfinding-on-block-update`

> Оптимальным значением является `false`.

#### `fix-climbing-bypassing-cramming-rule`

> Оптимальным значением является `true`.

#### `armor-stands-tick`

> Оптимальным значением является `false`.

#### `armor-stands-do-collision-entity-lookups`

> Оптимальным значением является `false`.

#### `tick-rates`

> Оптимальными значениями являются

> sensor: villager: secondarypoisensor: `80`

> sensor: villager: nearestbedsensor: `80`

> sensor: villager: villagerbabiessensor: `40`

> sensor: villager: playersensor: `40`

> sensor: villager: nearestlivingentitysensor: `40`

> behavior: villager: validatenearbypoi: `60`

> behavior: villager: acquirepoi: `120`.

#### `alt-item-despawn-rate`

каво блять

#### `use-faster-eigencraft-redstone`

> Оптимальным значением является `true`.

#### `disable-move-event`

> Оптимальным значением является `false`.

#### `mob-spawner-tick-rate`

> Оптимальным значением является `2`.

#### `optimize-explosions`

Данный параметр отвечает за оптимизацию взрывов.

> Оптимальным значением является `true`.

#### `enable-treasure-maps`

> Оптимальным значением является `false`.

#### `treasure-maps-return-already-discovered`

> Оптимальным значением является `true`.

#### `grass-spread-tick-rate`

> Оптимальным значением является `4`.

#### `container-update-tick-rate`

> Оптимальным значением является `1`.

#### `non-player-arrow-despawn-rate`

> Оптимальным значением является `20`.

#### `creative-arrow-despawn-rate`

> Оптимальным значением является `20`.

#### `anti-xray`

Данный параметр скрывает руду от читеров, использующих X-Ray. Включение данной опции будет снижать производительность сервера, однако, оно все же эффективнее плагинов на anti-xray. В большинстве случаях влияние на производительность незначительная. Для детальной настройки посмотритe [рекомендуемые настройки Stonar96](https://gist.github.com/stonar96/ba18568bd91e5afd590e8038d14e245e)

> Оптимальным значением является `true`.

#### `remove-corrupt-tile-entities`

> Оптимальным значением является `true`.

#### `nether-ceiling-void-damage-height`

> Оптимальным значением является `127`.

### [tuinity.yml](https://github.com/Tuinity/Tuinity/wiki/Config)

#### `use-new-light-engine`

Данная опция отвечает за использование продвинутого светового движка Starlight.

> Оптимальным значением является `true`.

### [airplane.air](https://github.com/TECHNOVE/Airplane/wiki)

#### `max-loads-per-projectile`

> Оптимальным значением является `8`.

#### `max-tick-freq`

> Оптимальным значением является `20`.

#### `activation-dist-mod` 

> Оптимальным значением является `7`.

### [purpur.yml](https://purpur.pl3x.net/docs/)

#### `use-alternate-keepalive`

You can enable Purpur's alternate keepalive system so players with bad connection don't get timed out as often. Has known incompatibility with TCPShield.

> Enabling this sends a keepalive packet once per second to a player, and only kicks for timeout if none of them were responded to in 30 seconds. Responding to any of them in any order will keep the player connected. AKA, it won't kick your players because 1 packet gets dropped somewhere along the lines  
~ https://purpur.pl3x.net/docs/Configuration/#use-alternate-keepalive

## Оптимизация операционной системы

### Linux

#### Использование демонов, повышающих производительность системы
* [Nohang](https://github.com/hakavlad/nohang)
* [Ananicy](https://github.com/Nefelim4ag/Ananicy)

#### Перевод процессора из энергосбережения в производительный режим

Debian/Ubuntu

`cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor`

`echo "performance" | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor` Sets profile to performance.

Arch

`sudo pacman -S cpupower`

`sudo cpupower frequency-set -g performance`

`sudo nano /etc/systemd/system/cpupower.service`

> [Unit]
Description=Set CPU governor to performance

> [Service]
Type=oneshot
ExecStart=/usr/bin/cpupower -c all frequency-set -g performance

> [Install]
WantedBy=multi-user.target

`sudo systemctl enable cpupower.service`

### Windows

#### Использование кастомного поверплана

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

Источники:
https://github.com/YouHaveTrouble/minecraft-optimization
https://docs.google.com/document/d/1IjTxl7LaPKJyRoLpGEhm4ptBhob_jRgLLQpMugS7qe8/edit#
.
.
.

# Common pitfalls and best practices

This article aims to explain common pitfalls that server owners face.

## Always backup
There are two types of people - those who make backups, and those who will start making backups. It's just a matter of time when you experience data loss. Always make copies to avoid losing your worlds or plugin data. You can apply this to any computer related workflow, not just minecraft.

## Don't use outdated software
By running outdated software versions you risk players abusing unpatched exploits, including item duplication (infinite items). It also adds an inconvenience factor since your players have to specifically downgrade their client version to match your server. This can be circumvented by using a protocol hack, but it's not ideal.

## Don't run Bukkit/Spigot anymore
Bukkit and Spigot are basically in maintenance mode. They update anytime there's a new version and if a critical exploit is found, but don't add any performance updates. This means any performance issues you may experience on those softwares will never be improved over time. To avoid that, upgrade to [Paper](https://papermc.io/downloads), [Tuinity](https://ci.codemc.io/job/Spottedleaf/job/Tuinity) or [Purpur](https://purpur.pl3x.net/downloads). Bukkit/Spigot plugins will work just as well (maybe even better) with the server software listed. If they don't, then it's safe to assume that the plugin dev is either doing things that they shouldn't or did a negligent job creating their plugin. They also add optimization patches like a chunk loading system that can take advantage of multiple cpu threads or a setting that allows the server to tick less chunks than it actually sends to the player. See the [main optimization guide](https://github.com/YouHaveTrouble/minecraft-optimization) for more details.

## Avoid shared hosting if possible
Shared hosts are usually the cheapest option, and that's for a valid reason. They offer you 2 types of resources - guaranteed and shared. Guaranteed resources are usually laughably low and may not be enough to run a server for a few players. Shared resources on the other hand are usually enough to run a server with decent performance. There is a catch, though; shared resources, like the name implies, are shared between your server and other servers on the same physical machine. Your server can only benefit from having them when no other server uses them. The situation where your server fully utilises shared resources is pretty much impossible to happen, as most shared hosts oversell their resources. Like airplane tickets, the hosting site sells more resources than they have available in hopes that not all of them will be used. This often leads to situations where all servers are bogged down because there aren't enough resources to spare.

## Avoid datapacks that use command functions
Datapacks that run commands are extremely laggy. It may not be much with a few players on, but that doesn't scale well with the playercount and will lag your server pretty quickly as you gain players. Datapacks that modify biomes, loot tables, etc are fine. You're better off looking for a plugin alternative.

## Choosing hardware
Don't just go off of how much RAM you need. You should instead focus on what kind of CPU you should use, since the CPU is the most important part of the server. You want something that [ranks good on single core performance](https://www.cpubenchmark.net/singleThread.html), as a server mainly runs on one thread. Multiple threads are utilised for quite some time now in systems like async chunk loading on paper, however.

You should absolutely avoid Hard Drives (HDDs). Their speeds are simply way too slow to justify running a server on them since minecraft is heavy on I/O operations (especially with high view distances and higher player counts). A Solid State drive (SSD) is a far better choice because of it's much faster I/O.
