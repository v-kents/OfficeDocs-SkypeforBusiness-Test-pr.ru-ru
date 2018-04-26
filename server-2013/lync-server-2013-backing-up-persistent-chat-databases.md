﻿---
title: Резервное копирование баз данных Persistent Chat
TOCTitle: Резервное копирование баз данных Persistent Chat
ms:assetid: b99ebdc0-a025-44d7-9d74-37a7365f330d
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ945646(v=OCS.15)
ms:contentKeyID: 52058325
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Резервное копирование баз данных Persistent Chat

 

_**Дата изменения раздела:** 2013-02-17_

Содержимое комнаты сохраняемый сеанс беседы хранится в базе данных сохраняемый сеанс беседы (Mgc.mdf). Это критически важные бизнес-данные, которые подлежат регулярному резервному копированию. Помимо содержимого комнаты чата в базе данных сохраняемый сеанс беседы также хранится информация о субъектах (например, пользователях и группах пользователей), их ролях и правах на доступ к комнатам чата.

Существуют два способа резервного копирования данных сохраняемый сеанс беседы.

  - Резервное копирование SQL Server

  - Командлет `Export-CsPersistentChatData`, который экспортирует данные сохраняемый сеанс беседы в виде файла

Для данных, которые создаются с помощью резервной копии SQL Server, требуется значительно больший объем дискового пространства (возможно, в 20 раз больше), чем объем, созданный `Export-CsPersistentChatData`, но, вероятнее всего, резервное копирование SQL является той процедурой, с которой уже знакомы администраторы.
