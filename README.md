# Гайд по созданию и настройке сервера Minecraft

Основан на [данном гайде](https://github.com/YouHaveTrouble/minecraft-optimization).

## Содержание

* [Хостинг](#Хостинг)

    * [Бесплатные хостинги](#Бесплатные-хостинги)
    * [Платные хостинги](#Платные-хостинги)
    * [Собственный компьютер в качестве хоста](#Собственный-компьютер-в-качестве-хоста)

* [Java](#Java)

    * [Аргументы запуска Java](#Аргументы-запуска-Java)

* [Выбор ядра сервера](#Выбор-ядра-сервера)

* [Выбор прокси-сервера](#Выбор-прокси-сервера)

* [Пре-генерация чанков](#Пре-генерация-чанков)

* [Конфигурация файлов](#Конфигурация-файлов)

    * [server.properties](#serverproperties)
    * [bukkit.yml](#bukkityml)
    * [spigot.yml](#spigotyml)
    * [paper.yml](#paperyml)
    * [tuinity.yml](#tuinityyml)
    * [airplane.yml](#airplaneyml)
    * [purpur.yml](#purpuryml)
    * [pufferfish.yml](#pufferfishyml)
    * [config.yml](#configyml)
    * [waterfall.yml](#waterfallyml)
    * [velocity.toml](#velocitytoml)

* [Работа в операционной системе](#Работа-в-операционной-системе)

    * [Linux](#Linux)

        * [Действия после установки системы](#Действия-после-установки-системы)
        * [Загрузка ядра сервера](#Загрузка-ядра-сервера)
        * [Создание бэкапов и их загрузка на облако](#Создание-бэкапов-и-их-загрузка-на-облако)
        * [Использование демонов, повышающих производительность системы](#Использование-демонов-повышающих-производительность-системы)
        * [Перевод процессора из энергосбережения в производительный режим](#Перевод-процессора-из-энергосбережения-в-производительный-режим)

* [Слишком хорошие плагины и моды, чтобы быть правдой](#Слишком-хорошие-плагины-и-моды-чтобы-быть-правдой)

    * [Плагины для удаления предметов через определенное количество времени](#Удаляющие-предметы-через-определенное-кол-во-времени)
    * [Плагины моб-стакеры](#Моб-стакеры)
    * [Плагины для включения или выключения других плагинов](#Включающие-или-выключащие-другие-плагины)
    * [Плагины для автоматических бэкапов](#Плагины-для-автоматических-бэкапов)
    * [Моды, добавляющие поддержку Bukkit API для Fabric или Forge](#Моды-добавляющие-поддержку-Bukkit-API-для-Fabric-или-Forge)

* [Мониторинг сервера](#Мониторинг-сервера)

    * [mspt](#mspt)
    * [timings](#timings)
    * [spark](#spark)

* [Полезные советы](#Полезные-советы)

    * [Всегда делайте бэкапы](#Всегда-делайте-бэкапы)
    * [Не используйте устаревшее ПО](#Не-используйте-устаревшее-ПО)
    * [Не используйте Bukkit или Spigot](#Не-используйте-Bukkit-или-Spigot)
    * [Избегайте shared-хостингов](#Избегайте-shared-хостингов)
    * [Избегайте датапаки, использующие команды](#Избегайте-датапаки-использующие-команды)
    * [Выбор железа](#Выбор-железа)

* [Источники информации](#Источники-информации)

## Хостинг

### Бесплатные хостинги

* [PloudOS](https://ploudos.com/en/)

Лучший из бесплатных хостингов. Поддерживает такие ядра, как Paper, Purpur и Tuinity. Позволяет ставить свои плагины, свои моды, свои карты.

* [Heroku](https://heroku.com)

Подробный [гайд](https://www.youtube.com/watch?v=EBzkSDBmaoU&t=130s) по запуску сервера на данном хостинге. 1.16.4 не потянет, даже не пытайтесь.

* [Aternos](https://aternos.org/:ru/)

В отличие от Heroku может кое-как вывозить 1.16.4. Всё. На этом плюсы заканчиваются, начинаются минусы в виде долгой очереди (раньше спокойно обходилось VPN, сейчас такое провернуть нельзя), отсутствия возможности поставить свои плагины, своё ядро, настроить конфигурационные файлы.

* [Minehut](https://minehut.com/)

Тот же самый Aternos, но очередь отсутствует, однако невозможно изменить версию и включить вход с пиратки.

### Платные хостинги

* [DigitalOcean](https://www.digitalocean.com/products/droplets/)
* [Hostinger](https://www.hostinger.ru/vps-hosting-servera)
* [RUVDS](https://ruvds.com/ru-rub)

### Собственный компьютер в качестве хоста

Если Вы хотите использовать собственный ПК в качестве хоста сервера, то Вам понадобится:

* Создать и запустить сервер;

> Вам нужно установить JDK, скачать ядро и на его основе создать сервер. Более подробная инструкция по созданию будет в пункте [Работа в операционной системе](#Работа-в-операционной-системе).

* Пробросить порты;

> Для проброса портов необходим белый IP. Пробросить порты по протоколу TCP можно через настройки роутера и/или брандмауэр.

> В случае, если имеется только NAT-овский айпи с блокировкой портов можно воспользоваться [Ngrok](https://ngrok.com/), [PortMap](https://portmap.io/), [LocalTunnel](https://localtunnel.github.io/www/), [различными VPN с возможностью открывать порты (Private Internet Access)](https://openvpn.net/), [IPv6 Port Forwarding](http://rubukkit.org/threads/ipv6-shag-v-buduschee-ili-obxodim-seryj-ip-bez-hamachi.35342/), ну или же попросить услугу Публичного Статического IP без блокировки портов у провайдера. Для счастливых обладателей роутеров Keenetic есть вариант [KeenDNS](https://help.keenetic.com/hc/ru/articles/360000400919-%D0%A1%D0%B5%D1%80%D0%B2%D0%B8%D1%81-%D0%B4%D0%BE%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D1%85-%D0%B8%D0%BC%D0%B5%D0%BD-KeenDNS) с использованием облачного IPv4. Также можете попробовать взять дешевый VPS за пару десятков рублей в месяц с выделенным IPv4, после чего поднять на нём VPN сервер (к примеру, OpenVPN Server).

* Доменный адрес (по желанию);

Если хотите подключаться к своему серверу по буквенному IP, то Вам понадобится зарегистрировать либо домен (бесплатно можно получить на [freenom](https://www.freenom.com/ru/index.html?lang=ru)), после чего на [cloudflare](https://www.cloudflare.com/ru-ru/) создать SRV-запись (если Вы используете Ngrok, SSH) или A-запись (если имеете статический айпи с возможностью открывать порты), либо сабдомен (бесплатно можно получить на [freedns.afraid](https://freedns.afraid.org/)) и там же создать A/SRV-запись.

Если у Вас имеется аккаунт с Microsoft Azure for Students, можете бесплатно получить домен на год на [name.com](https://www.name.com/azure?).

## Java

Для версии 1.17 или выше нужен JDK версии 16 или выше.

Рекомендуемые JDK:

* [OpenJDK](https://openjdk.java.net/)
* [AdoptOpenJDK](https://adoptopenjdk.net/installation.html?variant=openjdk16&jvmVariant=hotspot)
* [AmazonCorrettoJDK](https://aws.amazon.com/ru/corretto/)
* [AzulJDK](https://www.azul.com/downloads/?package=jdk)

### Аргументы запуска Java

Немаловажным шагом в настройке сервера является оптимизация аргументов запуска Java. По ссылке ниже Вы сможете найти оптимальные флаги для Вашего сервера.

[Оптимизация аргументов запуска сервера от hilltty](https://github.com/hilltty/hilltty-flags)

## Выбор ядра сервера

Рекомендуемые ядра:

* [Pufferfish](https://github.com/pufferfish-gg/Pufferfish) - самое производительное ядро на сегодняшний день. 1.17+.
* [Airplane](https://github.com/Technove/Airplane) - является одним из лучших в плане производительности и стабильности. Форк Paper. К сожалению, обновляться данное ядро доступно лишь на 1.16-1.17 версиях.
* [Purpur](https://github.com/pl3xgaming/Purpur) - обеспечивает производительность на уровне Airplane, имеет большое количество геймплейных изменений, продвинутую конфигурацию. Форк Airplane. 1.14+.
* [Paper](https://github.com/PaperMC/Paper) - одно из самых популярных ядер в Minecraft, обеспечивающее неплохую производительность. Форк Spigot. 1.8.8+.
* [SportPaper](https://github.com/Electroid/SportPaper) - отлично подходит под сервера с мини-играми, имеет более лучшую производительность в сравнении с Paper 1.8.9. 1.8.9.
* [NachoSpigot](https://github.com/CobbleSword/NachoSpigot) - отлично подходит под сервера с мини-играми, имеет более лучшую производительность в сравнении с Paper 1.8.9. Форк TacoSpigot. 1.8.9.
* [SpongeForge](https://www.spongepowered.org/downloads/spongeforge/stable/1.12.2) - ядро для тех, кто хочет использовать плагины Sponge и моды Forge вместе. 1.12.2.

Ядра, которые нужно обходить стороной:

* [Spigot](https://getbukkit.org/download/spigot) - форк CraftBukkit с улучшенной производительностью. На сегодняшний день уступает другим ядрам по производительности.
* [CraftBukkit](https://getbukkit.org/download/craftbukkit) - дефолтное ядро с возможностью ставить плагины. На сегодняшний день сильно уступает другим ядрам по производительности.
* [Yatopia](https://github.com/YatopiaMC/Yatopia) - во-первых, данное ядро больше не поддерживается, соответственно никаких фиксов багов или эксплоитов (даже критических, к примеру, CVE-2021-44228 Log4j) быть не может. Во-вторых, Ятопия является свалкой патчей со множества других ядер. В ядро запихнули всё, что только можно, отчего оно крайне нестабильное. Подробнее Вы можете узнать [здесь](https://github.com/kennytv/Yaptapia).
* [Sugarcane](https://github.com/SugarcaneMC/Sugarcane) - Yatopia 2.0.
* [Patina](https://github.com/PatinaMC/Patina) - Yatopia 2.0.
* [Mohist](https://mohistmc.com/) - ужасное ядро. Подробнее в этой [статье](https://essentialsx.net/do-not-use-mohist.html).
* [MCPC+](https://ru-minecraft.ru/plaginy-minecraft/10408-147-mcpc-ogranicheniy-v-modah-dlya-bukkita-bolshe-net.html) - нестабильное ядро.
* [CatServer](https://github.com/Luohuayu/CatServer) - Mohist 2.0.
* [Magma](https://github.com/magmafoundation/Magma) - Mohist 2.0.
* [Akarin](https://github.com/Akarin-project/Akarin) - хуже, чем Yatopia.

## Выбор прокси-сервера

Ядра, представляющие из себя прокси-сервер, позволяют объединять несколько серверов Minecraft в один с возможностью быстрого переключения игроков между ними посредством команды `/server <сервер>`.

Рекомендуемые ядра:

* [Velocity](https://velocitypowered.com/) - аналог BungeeCord с прекрасной стабильностью, невероятной производительностью и быстрыми фиксами багов/эксплоитов.
* [Waterfall](https://github.com/PaperMC/Waterfall/) - форк BungeeCord со множеством изменений.

## Пре-генерация чанков

Предварительная генерация чанков - один из важнейших шагов в улучшении производительности сервера. Во время перемещения по миру постоянно генерируются новые чанки, которые создают нагрузку на сервер, и обычно на слабых ПК это влечет за собой низкую скорость прогрузки чанков.

Предварительно прогрузить чанки можно следующим плагином:

* [Chunky](https://www.spigotmc.org/resources/chunky.81534/)

## Конфигурация файлов

**Ядра сервера**

### [server.properties](https://minecraft.fandom.com/Server.properties)

#### `view-distance`

#### `simulate-distance`

### [bukkit.yml](https://bukkit.gamepedia.com/Bukkit.yml)

#### `spawn-limits`

Ограничивает количество мобов на всём сервере. (Если включить [per-player-mob-spawns](#per-player-mob-spawns) в paper.yml, то будет ограничивать кол-во мобов для каждого игрока).

В группу `monsters` входят `blaze`, `cave_spider`, `creeper`, `drowned`, `elder_guardian`, `ender_dragon`, `enderman`, `endermite`, `evoker`, `ghast`, `giant`, `guardian`, `hoglin`, `husk`, `illusioner`, `magma_cube`, `phantom`, `piglin`, `piglin_brute`, `pillager`, `ravanger`, `shulker`, `silverfish`, `skeleton`, `slime`, `spider`, `stray`, `fex`, `vindicator`, `witch`, `wither`, `wither_skeleton`, `zoglin`, `zombie`, `zombie_villager`, `zombified_piglin`.

В группу `animals` входят `bee`, `cat`, `chicken`, `cow`, `donkey`, `fox`, `goat`, `horse`, `llama`, `mule`, `mooshroom`, `ocelot`, `panda`, `parrot`, `pig`, `polar_bear`, `rabbit`, `sheep`, `skeleton_horse`, `strider`, `trader_llama`, `turtle`, `wandering_trader`, `wolf`, `zombie_horse`.

В группу `water-animals` входят `dolphin`,  `squid`.

В группу `water-ambient` входят `cod`, `pufferfish`, `salmon`, `tropical_fish`.

В группу `ambient` входит `bat`.

> Оптимальными значениями являются 

> monsters: `35`;

> animals: `10`;

> water-animals: `5`;

> water-ambient: `10`;

> ambient: `2`.

#### `ticks-per`

Определяет, раз в сколько тиков сервер будет пытаться заспавнить моба.

> Оптимальными значениями являются

> monster-spawn: `4`;

> animal-spawns: `400`;

> water-spawns: `400`;

> water-ambient-spawns: `400`;

> water-underground-creature-spawns: `400`;

> ambient-spawns: `400`.

### [spigot.yml](https://www.spigotmc.org/wiki/spigot-configuration/)

#### `view-distance`

Это расстояние в чанках вокруг игрока, в котором может что-либо происходить. Это включает в себя плавку в печах, выращивание саженцев. Вы должны установить это значение именно в `spigot.yml`, так как оно заменяет значение из `server.properties` и может быть установлено для каждого мира.

> Оптимальным значением является `7`.

!!! С версии 1.18 это расстояние можно настроить в `server.properties` в пункте `simulation-distance`

#### `seed-structure`

Перед генерацией мира **НАСТОЯТЕЛЬНО РЕКОМЕНДУЮ** изменить сиды структур, чтобы игрокам было гораздо сложнее узнать сид методом reverse engineering.

#### `enable-zombie-pigmen-portal-spawns`

Определяет, будут ли пигмены спавнится в порталах в ад. Может сломать некоторые фермы золота.

#### `ticks-per`

Определяет за сколько тиков воронка может передать предмет.

> Оптимальными значениями являются

> hopper-transfer: `8`;

> hopper-check: `8`.

#### `mob-spawn-range`

Ограничивает диапазон появления мобов вокруг игрока.

> Оптимальным значением яляется `2`.

#### `entity-activation-range`

Дистанция обнаружения игрока. Уменьшение данных значений увеличивает производительность, но может сломать фермы мобов.

> Оптимальными значениями являются

> animals: `16`;

> monsters: `24`;

> raiders: `48`;

> misc: `8`;

> water: `8`;

> villagers: `16`;

> flying-monsters: `48`.

#### `entity-tracking-range`

Определяет дистанцию видимости мобов.

> Оптимальными значениями являются

> players: `48`

> animals: `48`

> monsters: `48`
      
> misc: `32`

> other: `64`.

#### `tick-inactive-villagers`

Отключение этого параметра улучшает производительность, но игрокам придется находится рядом с деревней для обновления торгов у жителей, а также это может вызвать проблемы с фермами железа на жителях.

#### `nerf-spawner-mobs`

Отвечает за ИИ мобов, появившихся из спавнеров. При включении данного параметра они ничего не будут делать. В воде они смогут плавать только когда будет включен параметр `spawner-nerfed-mobs-should-jump` в paper.yml.

#### `merge-radius`

Определяет дистанцию между одинаковыми предметами и сферами опыта, при увеличении которой они объединятся.

> Оптимальными значениями являются

> item: `3.5`

> exp: `4.0`.

### [paper.yml](https://paper.readthedocs.io/en/latest/server/configuration.html)

#### `no-tick-view-distance`

Данный параметр определяет расстояние в чанках вокруг игрока, которое будет прогружаться, но в котором ничего не будет происходить.

> Оптимальным значением является `12`.

#### `delay-chunk-unloads-by`

Определяет, через сколько выгрузится чанк (в секундах), если в нем отсутствуют игроки.

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

> Оптимальным значением является `true`.

#### `despawn-ranges`

> Оптимальными значениями являются

> soft: `32`

> hard: `96`.

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

> sensor: villager: secondarypoisensor: `80`;

> sensor: villager: nearestbedsensor: `80`;

> sensor: villager: villagerbabiessensor: `40`;

> sensor: villager: playersensor: `40`;

> sensor: villager: nearestlivingentitysensor: `40`;

> behavior: villager: validatenearbypoi: `60`;

> behavior: villager: acquirepoi: `120`.

#### `alt-item-despawn-rate`

> Оптимальными значениями являются 

> enabled: `true`;

> COBBLESTONE: `300`;

> NETHERRACK: `300`; 

> SAND: `300`;

> RED_SAND: `300`;

> GRAVEL: `300`;

> DIRT: `300`;

> GRASS: `300`;

> PUMPKIN: `300`;

> MELON_SLICE: `300`;

> KELP: `300`;

> BAMBOO: `300`;

> SUGAR_CANE: `300`;

> TWISTING_VINES: `300`;

> WEEPING_VINES: `300`;

> OAK_LEAVES: `300`;

> SPRUCE_LEAVES: `300`;

> BIRCH_LEAVES: `300`;

> JUNGLE_LEAVES: `300`;

> ACACIA_LEAVES: `300`;

> DARK_OAK_LEAVES: `300`;

> CACTUS: `300`;

> DIORITE: `300`;

> GRANITE: `300`;

> ANDESITE: `300`;

> SCAFFOLDING: `600`.

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

### [airplane.yml](https://github.com/TECHNOVE/Airplane/wiki)

#### `max-loads-per-projectile`

> Оптимальным значением является `8`.

#### `max-tick-freq`

> Оптимальным значением является `20`.

#### `activation-dist-mod` 

> Оптимальным значением является `7`.

### [purpur.yml](https://purpur.pl3x.net/docs/)

#### `use-alternate-keepalive`

Включение этого параметра позволит игрокам терять соединение с сервером не так часто. Имеются проблемы совместимости с TCPShield.

> Оптимальным значением является `true`.

#### `dont-send-useless-entity-packets`

Включение этой опции не позволяет серверу отправлять пустые пакеты перемещения сущности (по умолчанию сервер отправляет этот пакет для каждой сущности, даже если она не передвигается). Может вызывать некоторые проблемы с плагинами, которые используют сущности на стороне клиента.

Однако, при включении данной опции, серверу потребуется больше времени, чтобы проверить, должен ли он отправлять пакет, в сравнении с обычной постоянной отправкой пакетов. Проще говоря, после включения этого параметра на процессор возложится больше нагрузки.

> Оптимальным значением является `false`.

#### `aggressive-towards-villager-when-lagging`

Отключение этого параметра приведет к тому, что зомби перестанут нападать на жителей деревни при понижении TPS до определённого значения, установленного с помощью `lagging-threshold` в purpur.yml.

> Оптимальным значением является `false`.

#### `entities-can-use-portals`

По дефолту сущности могут проходить через портал, выключение данного параметра не позволит им этого сделать. 

#### `villager.brain-ticks`

Эта опция позволяет указать как часто (в тиках) жители будут работать своим мозгом для того, чтобы найти какой-либо путь до какого-либо места (к примеру, до кровати, или до рабочего места).

> Оптимальным значением является `2`.

#### `villager.lobotomize`

При включении жители, которые не смогли найти путь до рабочего места будут лишены ИИ. Тем не менее, они будут время от времени пополнять свои запасы.

> Оптимальным значением является `true`.

#### `disable-treasure-searching`

Запрещает дельфинам искать структуры используя метод, аналогичный методу карты сокровищ.

> Оптимальным значением является `true`.

#### `teleport-if-outside-border`

Позволяет телепортировать игрока к спавну сервера, если он находится за пределами границы мира, поскольку границу ванильного мира можно обойти, а урона, наносимого границей может не хватить для убийства игрока.

> Оптимальным значением является `true`.

### pufferfish.yml
___
**Прокси-сервера**

### config.yml

### waterfall.yml

### velocity.toml

## Работа в операционной системе

### Linux

#### Действия после установки системы

**Debian**

Для начала обновим списки пакетов и репозиториев.

$ `sudo apt-get update`

Теперь установим необходимое ПО, в том числе и Java, в моем случае я устанавливаю [OpenJDK](https://openjdk.java.net/) версии 17.

$ `sudo apt-get install git curl make fakeroot screen openjdk-17-jre -y`

Проверим корректность установки Java.

$ `java --version`

#### Загрузка ядра сервера

#### Использование демонов, повышающих производительность системы

* [Nohang](https://github.com/hakavlad/nohang)

Debian

$ `git clone https://github.com/hakavlad/nohang.git`

$ `cd nohang`

$ `sudo make install`

$ `sudo systemctl enable nohang`

$ `sudo systemctl start nohang`

Arch

$ `yay -S nohang`

$ `sudo systemctl enable nohang`

$ `sudo systemctl start nohang`

Fedora

$ `sudo dnf install nohang-desktop`

$ `sudo systemctl enable --now nohang-desktop.service`

* [Ananicy](https://github.com/Nefelim4ag/Ananicy)

Debian

$ `git clone https://github.com/Nefelim4ag/Ananicy.git`

$ `cd Ananicy`

$ `sudo make install`

$ `sudo systemctl enable ananicy`

$ `sudo systemctl start ananicy`

Arch

$ `yay -S ananicy`

$ `sudo systemctl enable ananicy`

$ `sudo systemctl start ananicy`

#### Перевод процессора из энергосбережения в производительный режим

Debian

$ `sudo apt-get install linux-cpupower`

$ `sudo cpupower frequency-set -g performance`

$ `sudo nano /etc/systemd/system/cpupower.service`

> [Unit]
Description=Set CPU governor to performance

> [Service]
Type=oneshot
ExecStart=/usr/bin/cpupower -c all frequency-set -g performance

> [Install]
WantedBy=multi-user.target

$ `sudo systemctl enable cpupower.service`

Arch

$ `sudo pacman -S cpupower`

$ `sudo cpupower frequency-set -g performance`

$ `sudo nano /etc/systemd/system/cpupower.service`

> [Unit]
Description=Set CPU governor to performance

> [Service]
Type=oneshot
ExecStart=/usr/bin/cpupower -c all frequency-set -g performance

> [Install]
WantedBy=multi-user.target

$ `sudo systemctl enable cpupower.service`

## Плагины

### Удаляющие предметы через определенное кол-во времени
Бесполезные плагины, поскольку в конфигурациях файлов сервера присутствуют такие параметры, как [merge radius](#merge-radius) и [alt-item-despawn-rate](#alt-item-despawn-rate), которые еще и настраиваются обширнее плагинов. Да и в случае с плагинами производительность будет хуже.

### Моб-стакеры

Моб-стакеры - это плагины, которые "объединяют" ближайших мобов одного типа вместе, чтобы снизить общее количество мобов. Например, вместо того, чтобы иметь 20 зомби в одном чанке, плагин заменит его одним зомби, представляющим 20. Если этот моб умирает, то возрождается ещё один из объединённых мобов.

Идея этих плагинов заключается в снижении нагрузки на сервер посредством уменьшения кол-ва мобов в чанке.

В более поздних версиях Minecraft'а в случае, если мобов мало, игра старается создать их больше. С плагином моб-стакера, когда мобы действительно спавнятся, они обычно просто объединяются с другими ближайшими мобами. Эта проблема приводит к бесконечному циклу спавна мобов, существенно нагружая сервер.

Подробнее можете узнать в [блоге me4502](https://madelinemiller.dev/blog/mob-stacker-problems/)

### Включающие или выключащие другие плагины

Плагин, включающий или отключающий другие плагины во время работы сервера, может вызывать фатальные ошибки. К слову, команда `/reload` страдает точно такими же проблемами, и Вы можете прочитать о них больше в [блоге me4502](https://madelinemiller.dev/blog/problem-with-reload/)

## Мониторинг сервера

### mspt

Ядро Paper добавляет новую команду `/mspt`, которая показывает Вам, сколько времени потребовалось серверу для вычисления последних тиков. Хорошими Minimal и Average значениями являются 50 и ниже.

### timings

В ядре Airplane `timings` по дефолту отключены, чтобы улучшить производительность.

Timings показывают "задачи", на которые ушло больше всего времени. Чтобы узнать тайминги Вашего сервера, Вам просто нужно вписать команду `/timings paste` и щелкнуть по выданной ссылке. Вы также можете поделиться этой ссылкой с другими людьми, чтобы они могли Вам помочь. Существует подробный [туториал от Aikar](https://www.youtube.com/watch?v=T4J0A9l7bfQ) о том, как их читать.
  
### spark

[Spark](https://github.com/lucko/spark) - это плагин, показывающий использование CPU и ОЗУ. Вы можете посмотреть [гайд](https://spark.lucko.me/docs/), как его использовать. Также есть [гайд](https://spark.lucko.me/docs/guides/Finding-lag-spikes) по тому, как находить причину фризов, пролагов.

## Полезные советы

### Всегда делайте бэкапы

Всегда есть шанс потерять данные. Поэтому делайте бэкапы. Вы можете использовать для этого плагин [AutoBackup](https://www.spigotmc.org/resources/autobackup.88209/)

### Не используйте устаревшее ПО

Запуская устаревшие версии программного обеспечения, Вы рискуете тем, что игроки будут злоупотреблять багами (включая различные дюпы предметов), эксплоитами. Это также добавляет некоторые неудобства, в виде того, что игрокам придется использовать устаревшие версии, чтобы смочь зайти на Ваш серверу. Этого, конечно же, можно избежать, используя ViaVersions, но там есть свои загвоздки.

### Не используйте Bukkit или Spigot
CraftBukkit и Spigot в данный момент в своих обновлениях лишь исправляют критические ошибки, никак не улучшая производительность. Причем делают они это довольно таки долго.

Просто пересядьте на нормальные ядра в виде [Airplane](https://airplane.gg/) или [Purpur](https://purpur.pl3x.net/downloads). 

### Избегайте shared-хостингов

Shared-хостинг - обычно самый дешевый вариант из хостингов, и на это есть веская причина. Они предлагают вам 2 типа ресурсов - гарантированные и общие. Гарантированных ресурсов обычно очень мало, и они могут не подходить под запуск сервера для нескольких игроков. А общие же ресурсы обычно достаточны для работы сервера с приличной производительностью. Однако есть загвоздка: общие ресурсы, как следует из названия, используются совместно вашим сервером и другими серверами на одной и той же физической машине. Ваш сервер может только выиграть от их наличия, если никакой другой сервер их не использует. Но ситуация, когда Ваш сервер полностью использует общие ресурсы, практически невозможна, поскольку большинство общих хостов перепродают свои ресурсы. Это аналогично тому, как авиакомпания продает билетов больше, чем доступно, в надежде, что не все из них будут использованы. Это часто приводит к ситуациям, когда все серверы зависают из-за нехватки ресурсов.

### Избегайте датапаки, использующие команды

Датапаки, которые юзают команды, очень сильно снижают производительность сервера. Используйте только те датапаки, которые лишь модифицируют биомы, крафты и т.п.

### Выбор железа

Определимся с платформой. 

У AMD актуальный на данный момент сокет - это AM4. Процессоры на архитектуре Zen 1 (Ryzen 1000 и Ryzen 2000 APU) и Zen 1+ (Ryzen 1200/1600 версии AF, Ryzen 2000 и Ryzen 3000 APU) имеют ужасную одноядерную производительность и высокое латенси (благодаря детдомовской шине данных Infinity Fabric, так как её скорость передачи данных напрямую зависит от пропускной способности ОЗУ). В Zen 2 (Ryzen 3000 + 4000 APU) провели некоторые работы с Infinity Fabric и одноядерной производительностью, но этого недостаточно (поскольку 10-е поколение Intel сливает эту помойку). Zen 3 (Ryzen 5000) покупать уже можно, он имеет отличную одноядерную производительность и неплохое латенси, а также, имеет предел частоты ОЗУ в 4133MHz (для сравнения - на Zen 1 и Zen 1+ был упор в 3466MHz и 3600MHz соответственно, на Zen 2 - 3866MHz). `Разгон ОЗУ присутствует даже на A320 чипсете (до 3200MHz), тем не менее, для R5 5600X рекомендую раскошелиться на Asrock B450/B450M Pro4 (K4 рескин Pro4, если хотите подсветку, то можете взять K4)/MSI B450 Gaming Plus MAX/ну или же на самую лучшую плату на B450 чипсете - **ASUS TUF Gaming B450M-PRO S**, для 5800X - GIGABYTE B550M AORUS PRO-P/ASROCK B550 STEEL LEGEND, для R9 5900x/R9 5950X - GIGABYTE B550 AORUS MASTER/MSI MEG B550 UNIFY-X. Помойки в виде X370/X470/X570 не рассматриваем.`

У Intel актуальный на данный момент сокет - LGA1700. Alder Lake вышел невероятно крутым, сливает Zen 3 что в играх, что в рабочих задачах, при этом стоит дешевле (у 12700K по MSRP меньше цена в сравнении с R9 5800X, при этом он запросто может [потягаться с R9 5900X в рабочих задачах](https://www.techpowerup.com/review/intel-core-i7-12700k-alder-lake-12th-gen/12.html). LGA1700, это, конечно, круто, но и про LGA1200 нужно упомянуть. 11-е поколение скип (да, оно имеет отличную одноядерную производительность (чуть выше, чем у 10), очень низкое латенси, но потолок частоты ОЗУ в 3733MHz всё портит (На Gear 1), да и цены на них, при сравнении с 10 поколением, конечно, расстраивают). Поэтому 10-е поколение выглядит самым оптимальным решением. Оно также имеет отличную одноядерную производительность, очень низкое латенси, при этом позволяет разгонять озу выше 3733MHz без делителей. `Разгон ОЗУ присутствует только на B560, Z490, Z590 чипсетах. Для 10100F/10400F рекомендую взять (если не нужен разгон ОЗУ - берите H410) B560, для 10600KF/10700KF - MSI Z490-A Pro, Для 10850K/10900KF - ASUS TUF Gaming Z490-Plus/GIGABYTE Z490 AORUS ELITE.`

Теперь нужно выбрать накопители.

Сервер лучше всего держать на SSD (Samsung 870 EVO/Kingston KC600/Crucial BX500) диске, желательно NVMe (WD Black SN850/Samsung 980 PRO/Samsung 980/SiliconPower P34A80/Kingston A2000/Kingston NV1 500GB).

# Источники информации

[Дискорд сервер PaperMC](https://discord.gg/papermc)
[Дискорд сервер Airplane](discord.gg/63dDSReB7j)
[Дискорд сервер Fabric](https://discord.gg/v6v4pMv)
[Гайд по оптимизации сервера от Paper Chan](https://eternity.community/index.php/paper-optimization/)
[Гайд по настройке bukkit.yml](https://bukkit.fandom.com/wiki/Bukkit.yml/ru)
[Ещё один гайд по настройке bukkit.yml](https://blog.airplane.gg/bukkit-configuration/)
[Гайд по настройке spigot.yml](https://www.spigotmc.org/wiki/spigot-configuration/)
[Гайд по настройке paper.yml](https://paper.readthedocs.io/en/latest/server/configuration.html)
[Гайд по настройке tuinity.yml](https://github.com/Tuinity/Tuinity/wiki/Config)
[Гайд по настройке airplane.yml](https://github.com/TECHNOVE/Airplane/wiki)
[Гайд по настройке категории Dynamic Entity Activation Range в airplane.yml](https://blog.airplane.gg/dear-configuration/)
[И снова гайд по настройке airplane.yml]()
[Настройка Waterfall](https://paper.readthedocs.io/en/latest/waterfall/configuration.html)
[Настройка Velocity](https://docs.velocitypowered.com/en/latest/users/configuration.html)
[Гайд по оптимизация Arch Linux от ventureoo](https://github.com/ventureoo/ARU)
