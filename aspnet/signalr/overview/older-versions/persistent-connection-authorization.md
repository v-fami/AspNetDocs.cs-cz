---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: Ověřování a autorizace trvalých připojení SignalR (SignalR 1.x) | Dokumentace Microsoftu
author: bradygaster
description: Toto téma popisuje, jak vynutit autorizaci na trvalé připojení. Obecné informace o integraci zabezpečení do aplikace SignalR...
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9ccc59e3ea502daf12ce82382ab30ca73ca0f9b5
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117044"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a>Ověřování a autorizace trvalých připojení SignalR (SignalR 1.x)

podle [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Toto téma popisuje, jak vynutit autorizaci na trvalé připojení. Obecné informace o integraci zabezpečení do aplikace funkci SignalR naleznete v tématu [Úvod do zabezpečení](index.md).

## <a name="enforce-authorization"></a>Vynutit autorizaci

K vynucení pravidel autorizace, při použití [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) je nutné přepsat `AuthorizeRequest` metody. Nelze použít `Authorize` atribut s trvalé připojení. `AuthorizeRequest` Metoda je volána rozhraním SignalR před každým požadavkem k ověření, že je uživatel oprávnění k provedení požadované akce. `AuthorizeRequest` Metoda není volána z klienta; místo toho ověření uživatele přes standardní ověřovací mechanismus vaší aplikace.

Následující příklad ukazuje, jak omezit požadavky na ověření uživatelé.

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

Můžete přidat libovolný vlastní autorizace logiku v metodě AuthorizeRequest; například kontroluje, zda uživatel patří do určité role.
