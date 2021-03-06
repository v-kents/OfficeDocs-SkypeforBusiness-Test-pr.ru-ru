﻿---
title: Общие сведения о маршрутизации на основе расположения для конференц-связи
TOCTitle: Общие сведения о маршрутизации на основе расположения для конференц-связи
ms:assetid: 8b86740e-db95-4304-bb83-64d0cbb91d47
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dn362815(v=OCS.15)
ms:contentKeyID: 56270579
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Общие сведения о маршрутизации на основе расположения для конференц-связи

 

_**Дата изменения раздела:** 2015-03-09_

Приложение "Конференц-связь с маршрутизацией на основе расположения" предоставляет механизм для предотвращения обхода оплаты ТСОП при проведении конференций Lync. Оно отслеживает активные конференции и применяет ограничения маршрутизации на основе расположения в соответствии с местонахождением пользователей Lync.

Приложение "Конференц-связь с маршрутизацией на основе расположения" определяет, следует ли применять к собранию Lync маршрутизацию на основе расположения, если выполняются следующие условия.

  - Для организатора собрания включена маршрутизация на основе расположения. Ограничения маршрутизации на основе расположения применяются только к конференциям, организованным пользователями, для которых включена маршрутизация на основе расположения.

  - Хотя бы один участник собрания должен являться конечной точкой ТСОП. Ограничения маршрутизации на основе расположения применяются только к конференциям, включающим конечные точки ТСОП.

  - Сетевой сайт, где находится шлюз ТСОП, используемый для подключения конференции к ТСОП, а также сетевые сайты, из которых подключаются организаторы и участники.

Приложение "Конференц-связь с маршрутизацией на основе расположения" запрещает подключение пользователей Lync и конечных точек ТСОП из разных сетевых сайтов к одной конференции. Если для организатора собрания включена маршрутизация на основе расположения, приложение конференц-связи применяет следующие ограничения.

  - Возможность присоединения конечных точек к собранию Lync зависит от того, какие конечные точки уже присоединились к конференции. Это ограничение меняется по мере того, как существующие конечные точки покидают конференцию, а новые присоединяются к ней. Если организаторы и участники присоединились к собранию Lync из одного сетевого сайта, то разрешено присоединение конечной точки ТСОП, другого участника из того же сетевого сайта, участника из другого сетевого сайта или участника из неизвестного сетевого сайта.

  - Если организаторы и участники присоединились к собранию из разных или неизвестных сетевых сайтов, конечной точке ТСОП запрещено присоединяться к собранию в случае, если звонок ТСОП поступает из магистрали SIP, для которой включена маршрутизация на основе расположения.

  - Если организаторы и участники присоединились к собранию из одного сетевого сайта и при этом имеются участники, которые присоединились к собранию из ТСОП, конечной точке Lync из другого сетевого сайта запрещено присоединяться к собранию.

Эти ограничения маршрутизации на основе расположения для конференц-связи обобщаются в приведенной ниже таблице.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Пользователи конференции на данный момент</p></td>
<td><p>Пользователи, которым разрешено присоединяться к конференции</p></td>
<td><p>Пользователи, которым запрещено присоединяться к конференции</p></td>
</tr>
<tr class="even">
<td><p>Пользователи клиента VoIP Lync из одного сетевого сайта</p></td>
<td><p>Пользователь клиента VoIP Lync из того же сетевого сайта</p>
<p>Пользователь клиента VoIP Lync из другого сетевого сайта</p>
<p>Пользователь клиента VoIP Lync из неизвестного сетевого сайта</p>
<p>Федеративный пользователь клиента VoIP Lync</p>
<p>Пользователь, присоединяющийся с помощью конечной точки ТСОП</p></td>
<td><p>Нет</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Пользователи клиента VoIP Lync из неизвестного сетевого сайта</p></td>
<td><p>Пользователь клиента VoIP Lync из любого сайта</p>
<p>Пользователь клиента VoIP Lync из неизвестного сайта</p>
<p>Федеративный пользователь клиента VoIP Lync</p></td>
<td><p>Пользователь, присоединяющийся с помощью конечной точки ТСОП</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Пользователи клиента VoIP Lync из других сетевых сайтов</p></td>
<td><p>Пользователь клиента VoIP Lync из любого сетевого сайта</p>
<p>Пользователь клиента VoIP Lync из неизвестного сетевого сайта</p>
<p>Федеративный пользователь клиента VoIP Lync</p></td>
<td><p>Пользователь, присоединяющийся с помощью конечной точки ТСОП</p></td>
</tr>
<tr class="odd">
<td><p>Пользователи клиента VoIP Lync из одного сетевого сайта и пользователи, присоединяющиеся с помощью конечной точки ТСОП</p></td>
<td><p>Пользователь клиента VoIP Lync из того же сетевого сайта</p>
<p></p></td>
<td><p>Пользователь клиента VoIP Lync из другого сетевого сайта</p>
<p>Пользователь клиента VoIP Lync из неизвестного сетевого сайта</p>
<p>Федеративный пользователь клиента VoIP Lync</p></td>
</tr>
</tbody>
</table>


Ниже перечислены дополнительные особенности приложения "Конференц-связь с маршрутизацией на основе расположения".

  - Если пользователю запрещено присоединяться к конференции из-за ограничений маршрутизации на основе расположения, его звонок будет отклонен, а в клиенте Lync появится сообщение о том, что звонок не был выполнен или завершился.

  - Конечной точке, присоединяющейся к конференции, в отношении которой действуют ограничения маршрутизации на основе расположения, будет разрешено присоединение вне зависимости от состояния, если конечная точка присоединяется через магистраль, для которой не включена маршрутизация на основе расположения.

  - К системе УАТС, подключенной к серверу-посреднику через магистраль SIP, не используемую для передачи исходящих звонков в ТСОП, будут применяться те же ограничения, что и к пользователям Lync сетевого сайта, в котором определена магистраль SIP. Например, конечная точка ТСОП сможет присоединиться к конференции с пользователем УАТС и пользователем Lync, если они относятся к одному сетевому сайту. Если же пользователь УАТС и пользователь Lync относятся к разным сетевым сайтам, конечной точке ТСОП будет запрещено присоединение к конференции.

