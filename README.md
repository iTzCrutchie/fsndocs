# FiveM-FSN-Framework
Public Roleplay Framework for FiveM.

## Installation
Install the required below resources. Set up mysql-async, and add this to your server.cfg:
```
ensure mysql-async
add_ace resource.fsn_main command.start allow
ensure fsn_main

[ENSURE ALL NON FSN_* RESOURCES HERE]
```

The framework is designed to create all the tables for you in your DB upon successful connection to your database. If your database is not connected or you are not running mysql-async or have no clue how to do that then search it. We wont provide support on correctly and succesfully connecting to your database

#### Alongside the FSN [resources](https://github.com/jamessc0tt/FiveM-FSN-Framework/blob/master/fsn_main/resources.txt), the "framework" is built to work with the below publicly available resources.
- [mysql-async](https://github.com/brouznouf/fivem-mysql-async)
- [interactsound](https://github.com/plunkettscott/interact-sound)
- [K9](https://github.com/xander1998/k9)
- [Luxart Vehicle Control](https://forum.cfx.re/t/release-luxart-vehicle-control/17304)
- [mhacking](https://github.com/GHMatti/FiveM-Scripts/tree/master/mhacking)
- [mythic notify](https://github.com/JayMontana36/mythic_notify)
- [nativeui](https://github.com/FrazzIe/NativeUILua)
- [tokovoip](https://github.com/Itokoyamato/TokoVOIP_TS3/releases)
- [xgc tunerchip](https://github.com/VoXzE/xgc-tunerchip)

#### Support / Issues / Feature Requests
This project is in active development, I intend to cover major/minor bugs and also implement features I like the idea of. Any issues you find please report via GitHub's issue section. For support installing/using the framework please contact us on our support discord: https://discord.gg/CNg73Xh

#### Requirements
- x86-64 system running Linux or Windows (7/2008 R2+), decent upstream connection.
- FiveM Reborn Server
- Local/Remote MySQL database server
- At **LEAST** 4GB disk space (including room for future updates) 
- MySQL Server

#### License
You are free to use/modify the "framework" in any way you see fit, remember to contribute any worthwile changes to the project with a merge request. Please do not distribute the project without my explicit permission. Do **NOT** remove the ":FSN: Framework by JamesSc0tt" on the character selection/creation screen.

## Site Pages

<!-- prettier-ignore-start -->

{% include list.liquid all=true %}

<!-- prettier-ignore-end -->


## Theme and License

https://jekyll-rtd-theme.rundocs.io

The theme is available as open source under the terms of the MIT License
