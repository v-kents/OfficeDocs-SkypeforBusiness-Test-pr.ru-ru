﻿---
title: Отслеживание использования службы Mobility Service и UCWA
TOCTitle: Отслеживание использования службы Mobility Service и UCWA
ms:assetid: 8389b37a-ca3e-4047-8b51-85bc07da87e8
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Hh690025(v=OCS.15)
ms:contentKeyID: 49310384
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Отслеживание использования службы Mobility Service и UCWA

 

_**Дата изменения раздела:** 2013-02-14_

Следует постоянно отслеживать ЦП и память, используемые службой Lync Server Mobility Service (Mcx) и веб-интерфейсом API объединенных коммуникаций (UCWA). Чтобы отслеживать использование, прибегите к одному из следующих способов:

**Для веб-интерфейса API объединенных коммуникаций (UCWA):**

  - **LyncUcwa** является рабочим процессом в диспетчере служб IIS. На панели **Рабочие процессы** изучите столбцы **ЦП %** и **Выделено (КБ)** (память).

  - Счетчики производительности **ЦП** и **Процессор**.

В большинстве развертываний ресурсы ЦП, задействованные UCWA, не должны в среднем превышать 15 %. Использование памяти не должно выходить за пределы, описанные в статье [Отслеживание границ объема памяти сервера](lync-server-2013-monitoring-for-server-memory-capacity-limits.md).

Помимо счетчиков использования ЦП и памяти можно использовать следующие счетчики производительности, которые позволят определить степень перегрузки сервера запросами:

  - **LS:WEB – Throttling and Authentication\\WEB – Total Requests in Processing** показывает количество веб-запросов сервера в очереди. Если этот счетчик достигает 10 000, последующие запросы завершаются с ошибкой "503 — служба недоступна".

  - **ASP.NET\\Requests Queued** (значение всегда должно быть равно нулю)

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>При достижении или превышении этих значений следует вернуться к планированию мощности и повторно выполнить расчет, чтобы определить правильные значения тактовой частоты ЦП, числа ядер и объема памяти для компьютеров, на которых размещаются веб-службы.</td>
</tr>
</tbody>
</table>


**Для службы Mobility Service (Mcx):**

  - **CSIntMcxAppPool** и **CSExtMcxAppPool** являются рабочими процессами в служб IIS. На панели **Рабочие процессы** изучите столбцы **ЦП %** и **Частные байты (КБ)** (память).

  - Счетчики производительности **ЦП** и **Процессор**.

В большинстве развертываний ресурсы ЦП, задействованные службой Mobility Service, не должны в среднем превышать 15 %. Использование памяти не должно выходить за пределы, описанные в статье [Отслеживание границ объема памяти сервера](lync-server-2013-monitoring-for-server-memory-capacity-limits.md).

Помимо счетчиков производительности ЦП и памяти можно использовать следующие счетчики производительности ASP.NET, которые позволят определить степень перегрузки сервера запросами.

  - **ASP.NET v2.0.50727\\Requests Current** показывает количество веб-запросов сервера в очереди. Если этот счетчик достигает 5 000, последующие запросы завершаются с ошибкой "503 — служба недоступна".

  - **ASP.NET\\Requests Queued** (значение всегда должно быть равно нулю)

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>При достижении или превышении этих значений следует вернуться к планированию мощности и повторно выполнить расчет, чтобы определить правильные значения тактовой частоты ЦП, числа ядер и объема памяти для компьютеров, на которых размещаются веб-службы.</td>
</tr>
</tbody>
</table>


## См. также

#### Концепции

[Отслеживание границ объема памяти сервера](lync-server-2013-monitoring-for-server-memory-capacity-limits.md)
