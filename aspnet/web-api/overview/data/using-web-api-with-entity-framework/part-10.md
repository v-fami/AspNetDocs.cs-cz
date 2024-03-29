---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: Publikujte aplikaci do Azure App Service v Azure | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59417361"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a>Publikujte aplikaci do Azure App Service v Azure

podle [Mike Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

V posledním kroku budete publikovat aplikaci do Azure. V Průzkumníku řešení klikněte pravým tlačítkem myši na projekt a vyberte **publikovat**.

![](part-10/_static/image1.png)

Kliknutím na **publikovat** vyvolá **publikování webu** dialogového okna. Pokud jste zaškrtli možnost **hostitel v cloudu** při prvním vytvoření projektu a pak připojení a nastavení jsou už nakonfigurovaná. V takovém případě stačí kliknout **nastavení** kartě a zaškrtněte &quot;spustit migrace Code First&quot;. (Pokud jste nezaškrtli **hostitel v cloudu** na začátku, postupujte podle pokynů v [další části](#new-website).)

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

K nasazení aplikace, klikněte na tlačítko **publikovat**. Můžete zobrazit průběh publikování v **aktivita publikování webu** okna. (Z **zobrazení** nabídce vyberte možnost **ostatní Windows**a pak vyberte **aktivita publikování webu**.)

![](part-10/_static/image4.png)

Po dokončení nasazení aplikace Visual Studio automaticky otevře výchozí prohlížeč na adresu URL nasazené webové stránky a aplikace, kterou jste vytvořili je nyní spuštěna v cloudu. Adresy URL v adresním řádku prohlížeče ukazuje, že lokality se načítá z Internetu.

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a>Nasazení na nový web

Pokud jste nekontrolovaly **hostitel v cloudu** při prvním vytvoření projektu, můžete nakonfigurovat novou webovou aplikaci nyní. V Průzkumníku řešení klikněte pravým tlačítkem myši na projekt a vyberte **publikovat**. Vyberte **profilu** kartě a klikněte na tlačítko **Microsoft Azure Websites**. Pokud ještě nejste momentálně do Azure, se výzva k přihlášení.

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

V **existující weby** dialogového okna, klikněte na tlačítko **nový**.

![](part-10/_static/image9.png)

Zadejte název lokality. Vyberte předplatné a oblast. V části **databázový server**vyberte **vytvořit nový Server**, nebo vyberte existující server. Klikněte na možnost **Vytvořit**.

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

Klikněte na tlačítko **nastavení** kartě a zaškrtněte &quot;spustit migrace Code First&quot;. Pak klikněte na tlačítko **publikovat**.

> [!div class="step-by-step"]
> [Předchozí](part-9.md)
