﻿---
title: 'Lync Server 2013: определение шлюза в построителе топологий'
TOCTitle: Определение шлюза в построителе топологий
ms:assetid: 456e5a96-d9f6-42a6-862c-a69464391628
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Gg425945(v=OCS.15)
ms:contentKeyID: 49309627
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Определение шлюза в построителе топологий в Lync Server 2013

 

_**Дата изменения раздела:** 2012-10-04_

Выполните действия, описанные в этом разделе, чтобы с помощью топологий определить *одноранговый узел* , с которым можно связать сервер посредник, чтобы предоставить пользователям с поддержкой корпоративной голосовой связи выход в ТСОП. Одноранговым узлом для посредник может быть шлюз ТСОП, IP-УАТС или пограничный контроллер сеансов (SBC) для поставщика услуг интернет-телефонии (ITSP), к которому вы подключаетесь при настройке SIP-магистрали.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>В данном разделе предполагается, что вы настроили, по крайней мере, один внутренний пул переднего плана или сервер Сервер Standard Edition хотя бы в одном центральном узле с совмещенным или изолированным сервером посредник, как описано в разделах <a href="lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md">Определение и настройка пула переднего плана или сервера Standard Edition в Lync Server 2013</a> и <a href="lync-server-2013-publish-the-topology.md">Публикация топологии в Lync Server 2013</a> документации по развертыванию. В данном разделе также предполагается, что вы проверили наличие в инфраструктуре необходимых компонентов, описанных в разделах <a href="lync-server-2013-software-prerequisites-for-enterprise-voice.md">Необходимое программное обеспечение для корпоративной голосовой связи в Lync Server 2013</a> и <a href="lync-server-2013-security-and-configuration-prerequisites-for-enterprise-voice.md">Необходимые условия для обеспечения безопасности и настройки корпоративной голосовой связи в Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


## Определение однорангового узла для сервера-посредника

1.  Запустите построитель топологий: нажмите кнопку **Пуск**, последовательно выберите пункты **Все программы** и **Microsoft Lync Server 2013** и щелкните элемент **Построитель топологий Lync Server**.

2.  В Lync Server 2013 выберите имя узла, щелкните "Общие компоненты", щелкните правой кнопкой узел **Шлюзы ТСОП** и выберите команду **Создать шлюз ТСОП** .
    
    ![Построитель топологии Lync Server 2013](images/Gg425945.d898c3c1-8798-4b74-8f02-b994ef3db4c1(OCS.15).png "Построитель топологии Lync Server 2013")

3.  В диалоговом окне **Определение нового шлюза IP/ТСОП** введите полное доменное имя или IP-адрес узла и нажмите кнопку **Далее** .
    
    ![Шлюз IP/ТСОП](images/Gg425945.8017ba5e-41bc-48d4-97d9-fd306cd322b8(OCS.15).png "Шлюз IP/ТСОП")
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Если вы выбрали TLS в качестве транспорта, необходимо указать полное доменное имя, а не IP-адрес узла посредник.</td>
    </tr>
    </tbody>
    </table>


4.  Определите режим прослушивания (IPv6 или IPv4) IP-адреса нового шлюза ТСОП и нажмите **Далее** .
    
    ![IP-адрес](images/Gg425945.c7fc0d12-adc8-45a7-aca1-b376e1d2fcec(OCS.15).png "IP-адрес")

5.  Определите *корневую магистраль* для шлюза ТСОП. Магистраль – это логическое соединение между сервером- посредник и шлюзом, которое определяется уникальным набором чисел.
    
    {полное доменное имя посредник, порт прослушивания посредник (TLS или TCP): IP-адрес и полное доменное имя шлюза, порт прослушивания шлюза}
    
      - При определении шлюза ТСОП в построителе топологий необходимо указать корневую магистраль, чтобы успешно добавить шлюз ТСОП в топологию.
    
      - Корневая магистраль не может быть удалена, пока не будет удален шлюз ТСОП.
    
    ![Определение шлюза: корневая магистраль](images/Gg425945.3b030757-eb35-4616-bb6b-74ee67507e3d(OCS.15).png "Определение шлюза: корневая магистраль")

6.  В разделе **Порт прослушивания для шлюза IP/ТСОП** введите порт прослушивания, который будет использоваться шлюзом, УАТС или SBC для SIP-сообщений от посредник который будет связан с корневой магистралью шлюза ТСОП. (По умолчанию используется порт 5066 для TCP и порт 5067 для TLS на шлюзе ТСОП, УАТС или SBC. В узле для обеспечения связи в филиалах в узле филиала порты по умолчанию — 5081 для TCP и 5082 для TLS.)

7.  В разделе **Транспортный протокол SIP** выберите тип транспорта, используемый одноранговым узлом, и нажмите кнопку **ОК** .
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>По причинам безопасности настоятельно рекомендуется развернуть узел в посредник, который может использовать TLS.</td>
    </tr>
    </tbody>
    </table>


8.  В разделе **Связанный посредник** выберите серверов-посредников, с которым нужно связать корневую магистраль этого шлюза ТСОП.

9.  В разделе **Связанный порт посредник** введите прослушивающий порт, используемый посредник для SIP-сообщений от этого шлюза.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Благодаря поддержке нескольких магистралей в Lync Server 2013 в посредник можно определить несколько сигнальных портов SIP, которые будут использоваться для связи с несколькими шлюзами ТСОП. При определении магистрали <strong>Связанный порт посредник</strong> должен находиться в пределах диапазона портов прослушивания для соответствующего протокола, разрешенного посредник. Этот диапазон портов определяется в Lync Server 2013 и пулах серверов-посредников. Нажмите правой кнопкой мыши необходимый пул серверов-посредников и выберите <strong>Изменить свойства</strong>. Укажите диапазон портов в поле <strong>Прослушивающие порты</strong> .</td>
    </tr>
    </tbody>
    </table>


10. Нажмите кнопку **Готово** .

<table>
<thead>
<tr class="header">
<th><img src="images/JJ618369.important(OCS.15).gif" title="important" alt="important" />Важно!</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Прежде чем завершить этот шаг, убедитесь, что определенный вами одноранговый узел работает и использует заданное полное доменное имя или IP-адрес.</td>
</tr>
</tbody>
</table>


Затем добавьте узел в топологию, выполните процедуры, описанные в разделе [Публикация топологии в Lync Server 2013](lync-server-2013-publish-the-topology.md) документации по развертыванию. Необходимо публиковать топологию при каждом использовании топологий для построения и или изменения топологии, чтобы можно было использовать данные для установки файлов для серверов с Lync Server.

## См. также

#### Задачи

[Изменение магистрали в построителе топологий в Lync Server 2013](lync-server-2013-modify-a-trunk-in-topology-builder.md)
