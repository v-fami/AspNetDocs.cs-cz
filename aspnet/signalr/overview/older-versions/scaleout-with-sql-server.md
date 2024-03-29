---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: Škálování aplikace SignalR SQL serverem (SignalR 1.x) | Dokumentace Microsoftu
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 8674b06a2a751c9a7b1c6c9b19782974d0602a62
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59386557"
---
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a>Škálování aplikace SignalR SQL Serverem (SignalR 1.x)

podle [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

V tomto kurzu použijete SQL Server k distribuci zpráv do aplikace SignalR, která je nasazená ve dvou samostatných instancí služby IIS. V tomto kurzu můžete spustit také na jeden testovací počítač, ale chcete-li získat plný vliv, je třeba nasadit aplikace SignalR pro dva nebo víc serverů. SQL Server musíte nainstalovat také na některý server nebo na samostatný vyhrazený server. Další možností je spustit kurz pomocí virtuálních počítačů v Azure.

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a>Požadavky

Microsoft SQL Server 2005 nebo novější. Propojovacího rozhraní podporuje počítače a serverové edice systému SQL Server. Nepodporuje se SQL Server Compact Edition nebo Azure SQL Database. (Pokud je vaše aplikace hostovaná v Azure, zvažte propojovací Service Bus rozhraní místo.)

## <a name="overview"></a>Přehled

Předtím, než získáme podrobný kurz, zde je rychlý přehled toho, co budete dělat.

1. Vytvoření nové prázdné databáze. Propojovacího rozhraní se vytvoří nezbytné tabulky v této databázi.
2. Přidejte tyto balíčky NuGet pro vaši aplikaci: 

    - [Microsoft.AspNet.SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft.AspNet.SignalR.SqlServer](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. Vytvoření aplikace SignalR.
4. Přidejte následující kód do souboru Global.asax konfigurace propojovacího rozhraní: 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a>Konfigurace databáze

Rozhodněte, zda bude aplikace používat ověřování Windows nebo ověřování systému SQL Server pro přístup k databázi. Bez ohledu na to Ujistěte se, že uživatel databáze má oprávnění k přihlášení, vytvoření schémat a vytvoření tabulky.

Vytvořte novou databázi pro propojovací rozhraní systému k použití. Databázi můžete přiřadit libovolný název. Není nutné vytvářet všechny tabulky v databázi. propojovacího rozhraní se vytvoří nezbytné tabulky.

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a>Povolí službu Service Broker

Doporučuje se povolí službu Service Broker pro databázi propojovacího rozhraní. Služba Service Broker poskytuje nativní podporu pro zasílání zpráv nebo řazení do fronty v systému SQL Server, které vám umožní efektivněji přijímat aktualizace propojovacího rozhraní. (Ale propojovacího rozhraní také funguje bez služby Service Broker.)

Pokud chcete zkontrolovat, zda je povolena služba Service Broker, dotazování **je\_zprostředkovatele\_povolené** sloupec v **zobrazení sys.databases** zobrazení katalogu.

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

Povolí službu Service Broker, pomocí následujícího dotazu SQL:

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> Pokud tento dotaz se zdá, zablokování, ujistěte se, že nejsou žádné aplikace, připojení k databázi.

Pokud jste povolili trasování, trasování zobrazí také, zda je povolena služba Service Broker.

## <a name="create-a-signalr-application"></a>Vytvoření aplikace SignalR

Vytvoření aplikace SignalR pomocí některé z těchto kurzů:

- [Začínáme s knihovnou SignalR](../getting-started/tutorial-getting-started-with-signalr.md)
- [Začínáme s knihovnou SignalR a MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)

V dalším kroku upravíme, aby byl chatovací aplikaci, aby podporovala škálování s využitím SQL serveru. Nejprve přidejte balíček SignalR.SqlServer NuGet do projektu. V aplikaci Visual Studio z **nástroje** příkaz **Správce balíčků NuGet**, vyberte **konzoly Správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

Dále otevřete soubor Global.asax. Přidejte následující kód, který **aplikace\_Start** metody:

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a>Nasazení a spuštění aplikace

Příprava vašich instancí Windows serveru k nasazení aplikace SignalR.

Přidejte roli služby IIS. Zahrnují funkce "Vývoj aplikací", včetně protokolu WebSocket.

![](scaleout-with-sql-server/_static/image4.png)

Zahrnují taky službu správy (uvedené v části "Nástroje pro správu").

![](scaleout-with-sql-server/_static/image5.png)

**Nainstalovat Web Deploy 3.0.** Když spustíte Správce služby IIS, vás vyzve k instalaci webové platformy společnosti Microsoft, nebo se dají [stáhněte instalační program](https://go.microsoft.com/fwlink/?LinkId=255386). Do platformy hledání pro nasazení webu a nainstalovat nasazení webu 3.0

![](scaleout-with-sql-server/_static/image6.png)

Zkontrolujte, že je spuštěná služby webové správy. Pokud ne, spusťte službu. (Pokud nevidíte v seznamu služeb Windows služby webové správy, ujistěte se, že jste nainstalovali službu pro správu při přidání IIS role.)

A konečně otevřete port 8172 pro protokol TCP. Toto je port, který používá nástroj nasazení webu.

Nyní jste připraveni k nasazení projektu sady Visual Studio z vývojového počítače k serveru. V Průzkumníku řešení klikněte pravým tlačítkem myši na řešení a klikněte na tlačítko **publikovat**.

Podrobnější dokumentaci k nasazení webu, najdete v článku [mapa obsahu webové nasazení pro Visual Studio a ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).

Pokud nasadíte aplikaci do dvou serverů, můžete otevřít každou instanci v samostatném okně prohlížeče a zobrazit, že každá z jiných příjem zpráv SignalR. (Samozřejmě v produkčním prostředí, dva servery strávil za nástrojem pro vyrovnávání zatížení.)

![](scaleout-with-sql-server/_static/image7.png)

Po spuštění aplikace, uvidíte, že SignalR vytvořila automaticky tabulky v databázi:

![](scaleout-with-sql-server/_static/image8.png)

Funkce SignalR spravuje tabulky. Tak dlouho, dokud je vaše aplikace nasazena, nemusíte odstraňovat řádky, úprava v tabulce a tak dále.
