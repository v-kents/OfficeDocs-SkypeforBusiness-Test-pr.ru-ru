﻿---
title: 'Lync Server 2013: заблокировано наследование разрешений для компьютеров, пользователей и контейнеров inetOrgPerson'
TOCTitle: Заблокировано наследование разрешений для компьютеров, пользователей и контейнеров inetOrgPerson
ms:assetid: c472ad21-a93d-4fcb-a3d9-60a2134a87fa
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Gg412970(v=OCS.15)
ms:contentKeyID: 49311110
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Заблокировано наследование разрешений для компьютеров, пользователей и контейнеров inetOrgPerson в Lync Server 2013

 

_**Дата изменения раздела:** 2014-12-19_

В заблокированном Доменные службы Active Directory объекты User и Computer часто помещаются в строго определенные организационные подразделения (OU) с отключенным наследованием разрешений для упрощения делегирования административных полномочий и включения использования объектов Group Policy (GPO) с целью реализации политик безопасности.

При подготовке домена и активации сервера устанавливаются элементы управления доступом (ACE) необходимые для Lync Server 2013. При отключении наследования разрешений группы безопасности Lync Server не будут наследовать эти элементы ACE. Если эти разрешения не наследуются, группы безопасности Lync Server не имеют доступа к параметрам и возникают следующие две проблемы:

  - Чтобы управлять объектами User, Contact, InetOrgPersons, а также серверами, группам безопасности Lync Server требуются элементы ACE, заданные в ходе процедуры подготовки домена для наборов свойств каждого пользователя, сеансов связи в реальном времени, объектов RTC User Search и Public Information. Когда наследование разрешений отключено, группы безопасности не наследуют эти элементы ACE и не могут управлять серверами и пользователями.

  - Для обнаружения серверов и пулов серверы, на которых работает Lync Server, используют элементы ACE, заданные при активации для связанных с компьютером объектов, включая Microsoft Container и Microsoft Server. Когда наследование разрешений отключено, группы безопасности, серверы и пулы не наследуют эти элементы ACE и не могут их использовать.

Для решения этих проблем в Lync Server имеется командлет **Grant-CsOuPermission**. Этот командлет задает необходимые элементы Lync Server ACE напрямую для заданного контейнера и организационных подразделений, а также объектов внутри контейнера и организационного подразделения.

## Установка разрешений для объектов User, InetOrgPerson и Contact после проведения подготовки домена

В заблокированной среде Active Directory с отключенным наследованием разрешений подготовка домена не ведет к установке необходимых элементов ACE для контейнеров или организационных подразделений внутри домена, содержащих объекты User или InetOrgPerson. В этом случае необходимо выполнить командлет **Grant-CsOuPermission** для каждого контейнера или организационного подразделения, содержащего объекты User или InetOrgPerson, для которых наследование разрешений отключено. При наличии топологии центрального леса эту процедуру также необходимо выполнить для контейнеров или организационных подразделений, содержащих объекты Contact. Дополнительные сведения о топологиях центрального леса см. в разделе [Поддерживаемые топологии Active Directory в Lync Server 2013](lync-server-2013-supported-active-directory-topologies.md) в документации по наличию поддержки. Объект ObjectType задает организационное подразделение.

Этот командлет добавляет необходимые элементы ACE непосредственно для заданных контейнеров или организационных подразделений и объектов User или InetOrgPerson внутри контейнера.

Для запуска этого командлета необходимы права пользователя, эквивалентные членству в группе администраторов домена. Если в заблокированной среде также были удалены элементы ACE прошедшего проверку подлинности пользователя, этой учетной записи необходимо предоставить элементы ACE для доступа на чтение для соответствующих контейнеров или организационных подразделений в корневом домене леса, как описано в разделе [Удаление разрешений пользователей, прошедших проверку подлинности в Lync Server 2013](lync-server-2013-authenticated-user-permissions-are-removed.md), или использовать учетную запись, которая является членом группы администраторов предприятия.

**Установка необходимых элементов ACE для объектов User, InetOrgPerson и Contact**

1.  Выполните вход на компьютер, присоединенный к домену, с использованием учетной записи, которая является членом группы администраторов домена или имеет эквивалентные права пользователя.

2.  Запустите командную консоль Lync Server: нажмите кнопку **Пуск**, последовательно выберите пункты **Все программы** и **Microsoft Lync Server 2013** и щелкните элемент **Командная консоль Lync Server**.

3.  Выполните следующую команду:
    
        Grant-CsOuPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> 
        -OU <DN name for the OU container relative to the domain root container DN> [-Domain <Domain FQDN>]
    
    Если параметр Domain не указан, значением по умолчанию является локальный домен.
    
    Например:
    
        Grant-CsOuPermission -ObjectType "User" -OU "cn=Redmond,dc=contoso,dc=net" -Domain "contoso.net"

4.  В файле журнала найдите результат выполнения **\<Success\>** в конце каждой задачи, чтобы убедиться, что разрешения были установлены, а затем закройте окно журнала. Либо выполните следующую команду, чтобы убедиться, что разрешения были установлены:
    
        Test-CsOuPermission -ObjectType <type of object> 
        -OU <DN name for the OU container relative to the domain root container DN> 
        [-Domain <Domain FQDN>] [-Report <fully qualified path and name of file to create>]
    
    Например:
    
        Test-CsOuPermission -ObjectType "User" -OU "cn=Redmond,dc=contoso,dc=net" -Domain "contoso.net" -Report "C:\Log\OUPermissionsTest.html"

## Установка разрешения для объектов Computer после проведения подготовки домена

В заблокированной среде Active Directory с отключенным наследованием разрешений подготовка домена не ведет к установке необходимых элементов ACE для контейнеров или организационных подразделений внутри домена, содержащих объекты Computer. В этом случае необходимо выполнить командлет **Grant-CsOuPermission** для каждого контейнера или организационного подразделения, где есть компьютеры, на которых выполняется Lync Server, с отключенным наследованием разрешений. Параметр ObjectType задает тип объекта.

Эта процедура добавляет необходимые элементы ACE непосредственно для указанных контейнеров.

Для запуска этого командлета необходимы права пользователя, эквивалентные членству в группе администраторов домена. Если также были удалены элементы ACE прошедшего проверку подлинности пользователя, этой учетной записи необходимо предоставить элементы ACE для доступа на чтение для соответствующих контейнеров в корневом домене леса, как описано в разделе [Удаление разрешений пользователей, прошедших проверку подлинности в Lync Server 2013](lync-server-2013-authenticated-user-permissions-are-removed.md), или использовать учетную запись, которая является членом группы администраторов предприятия.

**Установка необходимых элементов ACE для объектов Computer**

1.  Выполните вход на компьютер, присоединенный к домену, с использованием учетной записи, которая является членом группы администраторов домена или имеет эквивалентные права пользователя.

2.  Запустите командную консоль Lync Server: нажмите кнопку **Пуск**, последовательно выберите пункты **Все программы** и **Microsoft Lync Server 2013** и щелкните элемент **Командная консоль Lync Server**.

3.  Выполните следующую команду:
    
        Grant-CsOuPermission -ObjectType <Computer> 
        -OU <DN name for the computer OU container relative to the domain root container DN> 
        [-Domain <Domain FQDN>][-Report <fully qualified path and name of output report>]
    
    Если параметр Domain не указан, значением по умолчанию является локальный домен.
    
    Например:
    
        Grant-CsOuPermission -ObjectType "Computer" -OU "ou=Lync Servers,dc=litwareinc,dc=com" -Report "C:\Logs\OUPermissions.xml"

4.  В файле журнала данного примера, C:\\Logs\\OUPermissions.xml, найдите результат выполнения **\<Success\>** в конце каждой задачи и убедитесь в отсутствии ошибок, а затем закройте журнал.. Для проверки разрешений можно воспользоваться следующим командлетом:
    
        Test-CsOuPermission -ObjectType <type of object> 
        -OU <DN name for the OU container relative to the domain root container DN> [-Domain <Domain FQDN>]
    
    Например:
    
        Test-CsOuPermission -ObjectType "user","contact" -OU "cn=Bellevue,dc=contoso,dc=net" -Domain "contoso.net"
    
    > [!NOTE]  
    > При проведении подготовки корневого домена леса в заблокированной среде Active Directory помните, что Lync Server требуется доступ к контейнерам Active Directory Schema и Configuration.<br />    Если разрешение прошедшего проверку подлинности пользователя по умолчанию удаляется для контейнеров Schema или Configuration в AD DS, то доступ к указанному домену разрешен только членам группы администраторов схемы (для контейнера Schema) или администраторов предприятия (для контейнера Configuration). Поскольку командлетам Setup.exe, Командная консоль Lync Server и панели управления Lync Server требуется доступ к этим контейнерам, установка и развертывание средств администрирования завершится сбоем, если у пользователя, проводящего установку, не будет прав, эквивалентных членству в группе администраторов схемы или предприятия.<br />    Чтобы решить эту проблему, необходимо предоставить группе RTCUniversalGlobalWriteGroup доступ на чтение и запись к контейнерам Schema и Configuration.
