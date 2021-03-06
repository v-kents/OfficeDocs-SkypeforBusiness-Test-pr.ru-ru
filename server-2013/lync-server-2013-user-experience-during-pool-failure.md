﻿---
title: 'Lync Server 2013: действия пользователя в случае отказа пула'
TOCTitle: Действия пользователя в случае отказа пула
ms:assetid: b224b0d0-87e3-4cac-ae87-f45f54fabb49
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ205184(v=OCS.15)
ms:contentKeyID: 49310892
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Действия пользователя в случае отказа пула в Lync Server 2013

 

_**Дата изменения раздела:** 2015-03-09_

В случае отработки отказа пула все пользователи этого пула принудительно выходят из него и затем выполняют вход в резервный пул. В течение непродолжительного периода времени пользователи, выполнившие вход в резервный пул, могут находиться в режиме устойчивости. В этом режиме они не могут выполнять задачи, которые приводят к постоянному изменению данных в Lync Server, например добавление контактов. После завершения отработки отказа все пользователи могут использовать любые службы резервного пула.

При сбое пула все сеансы пользователя прерываются. Чтобы продолжить, пользователю потребуется повторно создать сеансы после отработки отказа.

В ходе отработки отказа или восстановления размещения пользователи не перемещаются. Пользователи, размещенные в сбойном пуле, временно обслуживаются резервным пулом. После восстановления исходного пула пользователи будут переведены на обслуживание исходным пулом.

Обратите внимание, что в Lync 2013 база данных сервера информирования о местонахождении не реплицируется на резервный пул. Администратору рекомендуется регулярно создавать резервные копии базы данных сервера информирования о местонахождении и использовать последнюю резервную копию для восстановления базы данных сервера в резервном пуле после отработки отказа.

## Взаимодействие с пользователями в ходе отработки отказа

Если пользователь находится в пуле, на котором произошел сбой, пользователь выходит из системы. Все одноранговые сеансы, в которых принимал участие пользователь, будут приостановлены, включая конференции, созданные пользователем. Пользователь не сможет выполнить вход до тех пор, пока не истечет время ожидания таймера устойчивости Регистратора или администратор не начнет процедуры аварийного восстановления, независимо от того, что произойдет раньше. Следующий вход пользователя будет осуществляться на резервном пуле. Если вход выполнен до завершения отработки отказа, то пользователи будут находиться в режиме устойчивости до завершения отработки отказа. После завершения отработки отказа пользователи смогут создать новые сеансы или восстановить предыдущие сеансы.

## Взаимодействие с пользователями в ходе восстановления размещения

Восстановление размещения может быть выполнено в то время, как затронутый пользователь выполнил вход в резервный пул. В ходе восстановления размещения пользователь остается в системе резервного пула и может продолжить работу. Обратите внимание на то, что на восстановление размещения требуется несколько минут. Так, для пула с 20 000 пользователей оно занимает приблизительно 60 минут.

В следующих таблицах приведены дополнительные сведения о состоянии затронутого пользователя клиента Lync 2013 или Microsoft Lync 2010 в ходе восстановления размещения и после него, а также сведения о том, как видят пользователя в пуле, в котором произошел сбой, пользователи остальных пулов. Пользователи клиента Microsoft Office Communicator 2007 R2 не могут выполнить вход, пока не будет завершена отработка отказа интерфейсного пула.

Термин *затронутый пользователь* относится к любому пользователю, который был переведен из основного пула и обслуживается резервным пулом. По определению пользователь, который изначально находился на резервном пуле, не является затронутым пользователем.

### Взаимодействие с затронутым пользователем пула в ходе восстановления размещения

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Состояние пользователя или задача</th>
<th>Во время восстановления размещения</th>
<th>После завершения восстановления размещения</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Состояние пользователя, который уже выполнил вход</p></td>
<td><p>Пользователь остается подключенным к резервному пулу. В определенный момент времени пользователь выйдет из системы и затем снова выполнит вход на исходном пуле в режиме устойчивости.</p></td>
<td><p>Состояние входа пользователя не изменяется и он переходит в обычный режим.</p></td>
</tr>
<tr class="even">
<td><p>Вход нового пользователя</p></td>
<td><p>Пользователь может выполнить вход в пул в режиме устойчивости.</p></td>
<td><p>Пользователь может выполнить вход в исходный пул в обычном режиме.</p></td>
</tr>
<tr class="odd">
<td><p>Текущие конференции, созданные затронутым пользователем</p></td>
<td><p>Все модальности конференции приостанавливаются. Кнопка &quot;Повторно присоединиться&quot; будет отображаться, но ни один пользователь не сможет присоединиться повторно, если затронутый пользователь находится в режиме устойчивости.</p></td>
<td><p>Все модальности работают. Для повторного присоединения к конференции участникам требуется нажать кнопку &quot;Повторно присоединиться&quot;.</p></td>
</tr>
<tr class="even">
<td><p>Текущие конференции, созданные незатронутым пользователем</p></td>
<td><p>Конференция будет продолжена и затронутый пользователь останется подключенным к конференции. Возможности затронутого пользователя в режиме устойчивости ограничены.</p></td>
<td><p>Конференция будет продолжена, затронутый пользователь останется подключенным к конференции, а все модальности начнут работу после выхода из режима устойчивости.</p></td>
</tr>
<tr class="odd">
<td><p>Создание расписания и изменение запланированных собраний, создание запланированных конференций</p></td>
<td><p>Невозможно в режиме устойчивости.</p></td>
<td><p>Доступно для всех модальностей.</p></td>
</tr>
<tr class="even">
<td><p>Сведения о присутствии, отображаемые остальным пользователям того же пула</p></td>
<td><p>Сведения о присутствии отсутствуют, если пользователь выполнил вход в резервный пул в режиме устойчивости.</p></td>
<td><p>Отображается последнее состояние присутствия, заданное пользователем, при этом изменения состояния присутствия не отображаются.</p></td>
</tr>
<tr class="odd">
<td><p>Доступность списка контактов и службы адресной книги</p></td>
<td><p>Недоступно</p></td>
<td><p>Доступно</p></td>
</tr>
<tr class="even">
<td><p>Все одноранговые сеансы и модальности</p></td>
<td><p>Доступно</p></td>
<td><p>Доступно</p></td>
</tr>
</tbody>
</table>


### Взаимодействие с пользователями, размещенными в незатронутом пуле, в ходе восстановления размещения другого пула

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Задача пользователя</th>
<th>Во время восстановления размещения</th>
<th>После завершения восстановления размещения</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Просмотр сведений о присутствии затронутого пользователя</p></td>
<td><p>Отображается последнее состояние присутствия, заданное затронутым пользователем.</p></td>
<td><p>Незатронутые пользователи могут просматривать обновленные сведения о присутствии затронутых пользователей.</p></td>
</tr>
<tr class="even">
<td><p>Текущие конференции, созданные затронутым пользователем</p></td>
<td><p>Все модальности конференции приостанавливаются.</p></td>
<td><p>Все модальности работают. Для повторного присоединения к конференции участникам требуется нажать кнопку &quot;Повторно присоединиться&quot;.</p></td>
</tr>
<tr class="odd">
<td><p>Текущие конференции, созданные незатронутым пользователем</p></td>
<td><p>Конференция будет продолжена, затронутый пользователь может остаться в конференции и все модальности будут работать.</p></td>
<td><p>Конференция будет продолжена, затронутый пользователь может остаться в конференции и все модальности будут работать.</p></td>
</tr>
<tr class="even">
<td><p>Все одноранговые сеансы и модальности</p></td>
<td><p>Доступно</p></td>
<td><p>Доступно</p></td>
</tr>
</tbody>
</table>

