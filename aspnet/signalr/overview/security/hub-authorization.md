---
uid: signalr/overview/security/hub-authorization
title: Ověřování a autorizace Center SignalR | Dokumentace Microsoftu
author: bradygaster
description: Toto téma popisuje, jak omezit, kteří uživatelé nebo rolí se dostanete metod rozbočovače. Verze softwaru použitým v tomto tématu ve Visual Studio 2013 .NET 4.5 SignalR...
ms.author: bradyg
ms.date: 01/05/2015
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 5006af5e623da6958a6d59949c6f2cf776c77fc3
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65113617"
---
# <a name="authentication-and-authorization-for-signalr-hubs"></a>Ověřování a autorizace center SignalR

podle [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Toto téma popisuje, jak omezit, kteří uživatelé nebo rolí se dostanete metod rozbočovače.
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru použitým v tomto tématu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - Funkce SignalR verze 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Předchozích verzích tohoto tématu
>
> Informace o předchozích verzích systému SignalR naleznete v tématu [starší verze funkce SignalR](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Otázky a komentáře
>
> Napište prosím zpětnou vazbu o tom, jak vám líbilo v tomto kurzu a co můžeme zlepšit v komentářích v dolní části stránky. Pokud máte nějaké otázky, které přímo nesouvisejí, najdete v tomto kurzu, můžete je publikovat [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Přehled

Toto téma obsahuje následující oddíly:

- [Povolit atribut](#authorizeattribute)
- [Vyžadovat ověřování pro všechna centra](#requireauth)
- [Vlastní autorizace](#custom)
- [Předat ověřovací informace pro klienty](#passauth)
- [Možnosti ověřování pro klienty .NET](#authoptions)

    - [Soubor cookie ověřování pomocí formulářů](#cookie)
    - [Ověřování Windows](#windows)
    - [Připojení záhlaví](#header)
    - [Certifikát](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a>Povolit atribut

Funkce SignalR poskytuje [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) atribut určit, které uživatele nebo role mají přístup do centra nebo metody. Tento atribut je umístěn v `Microsoft.AspNet.SignalR` oboru názvů. Můžete použít `Authorize` atribut rozbočovač nebo konkrétní metody v rozbočovači. Pokud použijete `Authorize` atribut třídy rozbočovače, požadavek na autorizaci zadané platí pro všechny metody v rozbočovači. Toto téma obsahuje příklady různých typů ověření požadavků, které můžete použít. Bez `Authorize` atribut připojeného klient může získat všechny veřejné metody v rozbočovači.

Pokud jste definovali role ve vaší webové aplikaci s názvem "Admin", můžete zadat, že jenom uživatelé v této roli můžete přístup k centru s následujícím kódem.

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

Nebo můžete určit, že Centrum obsahuje jednu metodu, která je k dispozici všem uživatelům a druhá metoda, která je pouze ověřeným uživatelům k dispozici, jak je znázorněno níže.

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

Následující příklady různých autorizace situacích:

- `[Authorize]` – jen ověření uživatelé
- `[Authorize(Roles = "Admin,Manager")]` – jen ověření uživatelé v zadaných rolí
- `[Authorize(Users = "user1,user2")]` – pouze pro ověřené uživatele s ze zadaných uživatelských jmen
- `[Authorize(RequireOutgoing=false)]` – pouze pro ověřené uživatele můžete vyvolat centra, ale volání ze serveru zpátky do klientů nejsou omezeny autorizace, jako je třeba když jenom určitým uživatelům můžete odeslat zprávu, ale všechny ostatní zprávy. Vlastnost RequireOutgoing dá používat jedině pro celé centrum není pro jednotlivce metody v rozbočovači. Když RequireOutgoing není nastavená na hodnotu false, jenom uživatelé, kteří splní požadavek na autorizaci se nazývají ze serveru.

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a>Vyžadovat ověřování pro všechna centra

Můžete vyžadovat ověřování pro všechny rozbočovače a metody ve vaší aplikaci pomocí volání [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) metoda při spuštění aplikace. Tuto metodu můžete použít, když máte více rozbočovače a chcete vynutit požadavek na ověření pro všechny z nich. S touto metodou nelze zadat požadavky pro role, uživatele nebo odchozí autorizace. Můžete zadat pouze omezen přístup k metodám centra ověřeným uživatelům. Atribut Authorize však můžete použít na rozbočovače a metody zadat další požadavky. Všechny požadavky, které zadáte v atributu je přidán do základní požadavek ověřování.

Následující příklad ukazuje spouštěcí soubor, který omezuje všech metod rozbočovače na ověřeným uživatelům.

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

Při volání `RequireAuthentication()` metoda po zpracování žádost SignalR, vyvolá výjimku SignalR `InvalidOperationException` výjimky. Funkce SignalR vyvolá tuto výjimku, protože modul nelze přidat do kanálu rozbočovače přidán po zavolání kanálu. Předchozí příklad ukazuje volání `RequireAuthentication` metodu `Configuration` metodu, která provádí jednou před prvního požadavku na zpracování.

<a id="custom"></a>

## <a name="customized-authorization"></a>Vlastní autorizace

Pokud je potřeba upravit, jak se určují autorizaci, můžete vytvořit třídu, která je odvozena z `AuthorizeAttribute` a přepsat [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) metody. Pro každý požadavek SignalR volá tuto metodu za účelem určení, zda je uživatel oprávnění k dokončení požadavku. Přepsané metody poskytují logiku potřebnou pro váš scénář autorizace. Následující příklad ukazuje, jak vynutit autorizaci prostřednictvím založené na deklaracích identity.

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a>Předat ověřovací informace pro klienty

Budete muset použít informace o ověřování v kódu, který běží na straně klienta. Předáním požadovaných informací při volání metody na straně klienta. Například metoda aplikace chat mohli předat jako parametr uživatelské jméno osoby, odesílání zpráv, jak je znázorněno níže.

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

Nebo můžete vytvořit objekt reprezentující informace o ověřování a tento objekt předat jako parametr, jak je znázorněno níže.

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

Nikdy byste neměli předávat id připojení pro jednoho klienta jiným klientům, protože ji uživatel se zlými úmysly třeba použít tak, aby napodoboval žádosti od tohoto klienta.

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a>Možnosti ověřování pro klienty .NET

Pokud máte klienta .NET, jako je například konzolové aplikace, která komunikuje s rozbočovači, který je omezen na ověřené uživatele, můžete předat přihlašovacími údaji v souboru cookie, záhlaví připojení nebo certifikát. Příklady v této části ukazují, jak použít tyto různé metody pro ověřování uživatele. Nejsou plně funkční aplikace SignalR. Další informace o klientech .NET s knihovnou SignalR naleznete v tématu [pokyny k rozhraní API Center – klient .NET](../guide-to-the-api/hubs-api-guide-net-client.md).

<a id="cookie"></a>

### <a name="cookie"></a>Soubor cookie

Při vašeho klienta .NET interakci s rozbočovači, který používá ověřování pomocí formulářů ASP.NET, musíte ručně nastavit ověřovacího souboru cookie pro připojení. Přidání souboru cookie `CookieContainer` vlastnost [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) objektu. Následující příklad ukazuje konzolovou aplikaci, která načte soubor cookie ověřování z webové stránky a přidá tento soubor cookie pro připojení.

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

Konzolová aplikace odesílá pověření, která mají <strong>www.contoso.com/RemoteLogin</strong> který může odkazovat na prázdnou stránku, která obsahuje následující soubor kódu na pozadí.

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a>Ověřování systému Windows

Pokud používáte ověřování Windows, můžete předat přihlašovacích údajů aktuálního uživatele pomocí [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) vlastnost. Nastavit přihlašovací údaje pro připojení k hodnotě DefaultCredentials.

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a>Připojení záhlaví

Pokud vaše aplikace nepoužívá soubory cookie, můžete předat informace o uživateli v hlavičce připojení. Můžete například předat token v hlavičce připojení.

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

Poté v rozbočovači, bude ověřit token uživatele.

<a id="certificate"></a>

### <a name="certificate"></a>Certifikát

Můžete předat klientský certifikát k ověření uživatele. Přidání certifikátu při vytváření připojení. Následující příklad ukazuje jenom postup přidání klientský certifikát pro připojení. nezobrazuje se úplná konzolovou aplikaci. Používá [certifikátu x 509](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) třída, která poskytuje několik způsobů vytvoření certifikátu.

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
