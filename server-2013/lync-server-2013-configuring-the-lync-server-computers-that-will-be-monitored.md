﻿---
title: Настройка компьютеров Lync Server для мониторинга
TOCTitle: Настройка компьютеров Lync Server для мониторинга
ms:assetid: 9f1b2b91-d5af-42ad-a27d-b0815f762ad8
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ205118(v=OCS.15)
ms:contentKeyID: 49310692
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Настройка компьютеров Lync Server для мониторинга

 

_**Дата изменения раздела:** 2012-10-20_

Поскольку Lync Server 2013 не использует процесс централизованного обнаружения, используемый в Microsoft Lync Server 2010, каждый компьютер Lync Server 2013, за которым планируется наблюдать, должен иметь возможность самостоятельно сообщать о своем существовании на сервер управления. Для этого необходимо установить файлы агента Operations Manager на каждый отслеживаемый компьютер. После установки файлов агента необходимо настроить компьютер для работы в качестве прокси-сервера System Center. Обратите внимание, что эти процедуры должны быть выполнены после установки и настройки Lync Server на этих компьютерах.
