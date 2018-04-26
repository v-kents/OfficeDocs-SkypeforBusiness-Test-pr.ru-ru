﻿---
title: 'Lync Server 2013: создание объектов Contact для размещенной единой системы обмена сообщениями Exchange'
TOCTitle: Создание объектов Contact для размещенной единой системы обмена сообщениями Exchange
ms:assetid: a39be52f-488a-4523-ad5f-ce1f0d681959
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Gg412765(v=OCS.15)
ms:contentKeyID: 49310736
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Создание объектов Contact для размещенной единой системы обмена сообщениями Exchange в Lync Server 2013

 

_**Дата изменения раздела:** 2012-09-24_

В этом разделе описывается создание контактных объектов автосекретаря или абонентского доступа для размещенной единой системы обмена сообщениями Exchange.

Подробные сведения см. в разделе [Управление объектом Contact в размещенной системе Exchange в Lync Server 2013](lync-server-2013-hosted-exchange-contact-object-management.md) документации по планированию.

Дополнительные сведения о настройке контактных объектов см. в документации Командная консоль Lync Server по следующим командлетам:

  - [New-CsExUmContact](new-csexumcontact.md)

  - [Set-CsExUmContact](set-csexumcontact.md)

<table>
<thead>
<tr class="header">
<th><img src="images/JJ618369.important(OCS.15).gif" title="important" alt="important" />Важно!</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Перед включением контактных объектов Lync Server 2013 для размещенной единой системы обмена сообщениями Exchange необходимо развернуть политику маршрутизации размещенной голосовой почты, применяемую к ним. Дополнительные сведения см. в разделе <a href="lync-server-2013-hosted-voice-mail-policies.md">Политики размещенной голосовой почты в Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


## Создание контактных объектов автосекретаря или абонентского доступа для размещенной единой системы обмена сообщениями Exchange

1.  Запустите командную консоль Lync Server: нажмите кнопку **Пуск**, последовательно выберите пункты **Все программы** и **Microsoft Lync Server 2013** и щелкните элемент **Командная консоль Lync Server**.

2.  Чтобы создать любой контактный объект, необходимо выполнить командлет New-CsExUmContact. Например, для создания контактного объекта автосекретаря и абонентского доступа выполните следующие командлеты:
    
        New-CsExUmContact -SipAddress "sip:exumaa1@fabrikam.com" -RegistrarPool "RedmondPool.litwareinc.com" -OU "HostedExUM Integration" -DisplayNumber "+14255550101" -AutoAttendant $True
    
        New-CsExUmContact -SipAddress "sip:exumsa1@fabrikam.com" -RegistrarPool "RedmondPool.litwareinc.com" -OU "HostedExUM Integration" -DisplayNumber "+14255550101"
    
    В этих примерах используются следующие параметры:
    
      - **SipAddress** указывает SIP-адрес контактного объекта. В качестве значения необходимо использовать адрес, который еще не использовался для настройки пользователя или контактного объекта в доменных службах Active Directory. Значение необходимо указывать в формате "sip:\< *SIP-адрес* \>", как показано в предыдущих примерах.
    
      - **RegistrarPool** указывает полное доменное имя пула, в котором выполняется служба регистратора.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Контактные объекты единой системы обмена сообщениями Exchange не могут перемещаться в пулы, которые являются частью развертываний Lync Server 2013, использующих версии до Lync Server 2013.</td>
        </tr>
        </tbody>
        </table>
    
      - **OU** задает подразделение Active Directory, в котором будет находиться данный контактный объект.
    
      - **DisplayNumber** указывает номер телефона контактного объекта. Номер телефона для каждого контактного объекта должен быть уникальным.
    
      - **AutoAttendant** указывает, является ли данный контактный объект автосекретарем. Автосекретарь предоставляет набор голосовых приглашений, которые позволяют звонящим перемещаться по телефонной системе, чтобы найти требуемого абонента. Значение **False** (по умолчанию) для этого параметра указывает контактный объект абонентского доступа.
