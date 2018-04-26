﻿---
title: Проверка репликации параметров конфигурации
TOCTitle: Проверка репликации параметров конфигурации
ms:assetid: 81a3c21d-b28a-4287-adac-11791e8db56d
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ205042(v=OCS.15)
ms:contentKeyID: 49310345
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Проверка репликации параметров конфигурации

 

_**Дата изменения раздела:** 2012-10-19_

Вы можете проверить репликацию данных конфигурации на пограничный сервер, выполнив командлет Lync Server 2013**Get-CsManagementStoreReplicationStatus** на внутреннем компьютере, на котором расположено центральное хранилище управления, или на любом присоединенном к домену компьютере, на котором установлены основные компоненты Lync Server 2013.

В начальных результатах для репликации может быть указано состояние "False" вместо "True". В этом случае выполните командлет **Invoke-CsManagementStoreReplication** и дождитесь завершения репликации, после чего еще раз выполните командлет **Get-CsManagementStoreReplicationStatus**.
