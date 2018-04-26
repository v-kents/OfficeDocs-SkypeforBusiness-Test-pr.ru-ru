﻿---
title: Настройка базы данных местоположений в Lync Server 2013
TOCTitle: Настройка базы данных местоположений в Lync Server 2013
ms:assetid: 8544be31-6958-47ef-b926-fdc80d56191c
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Gg398679(v=OCS.15)
ms:contentKeyID: 49310385
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Настройка базы данных местоположений в Lync Server 2013

 

_**Дата изменения раздела:** 2012-09-17_

Чтобы включить автоматическое определение клиентами своего местоположения в сети, сначала необходимо настроить базу данных местоположений. Если не настроить эту базу данных и задать для параметра **Требуется местоположение** в политике местоположений значение **Да** или **Отказ**, пользователь получит запрос на ручной ввод местоположения.

Чтобы настроить базу данных местоположений, следует выполнить следующие задачи.

1.  Заполните базу данных с сопоставлением сетевых элементов местоположениям. При использовании шлюза ELIN необходимо включить ELIN в поле \<Имя\_компании\>.

2.  Поверьте адрес по руководству MSAG, которое поддерживается поставщиком услуг E9-1-1.

3.  Опубликуйте обновленную базу данных.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Кроме того, можно определить дополнительную базу данных местоположений, которую можно использовать вместо базы данных местоположений. Подробности см. в разделе <a href="lync-server-2013-configure-a-secondary-location-information-service.md">Настройка службы сведений о дополнительном расположении в Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


## Содержание

  - [Наполнение базы данных местоположений](lync-server-2013-populate-the-location-database.md)

  - [Проверка адресов](lync-server-2013-validate-addresses.md)

  - [Публикация базы данных местоположений в Lync Server 2013](lync-server-2013-publish-the-location-database.md)
