---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: 'Postup: Vytvoření vlastní pomocné rutiny HTML pro aplikaci MVC? | Dokumenty Microsoft'
author: rick-anderson
description: V tomto videu pixelů na Chris ukazuje, jak vytvořit vlastní HtmlHelper, který není k dispozici ve standardní sady v aplikaci MVC. První, aplikace MVC ukázka...
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 60953243d3038667e4f729b1394e68f0c9d7c178
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59415047"
---
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a>Postup: Vytvoření vlastní pomocné rutiny HTML pro aplikaci MVC?

podle [Chris pixelů na](https://twitter.com/chrispels)

V tomto videu pixelů na Chris ukazuje, jak vytvořit vlastní HtmlHelper, který není k dispozici ve standardní sady v aplikaci MVC. Nejprve ukázkové aplikace MVC se vytvoří s ukázka kontroler a zobrazení k testování vlastních HtmlHelper. V dalším kroku se vytvoří modul s veřejné funkce, která je metodu rozšíření, která představuje implementaci vlastní HtmlHelper. Je vlastního pomocného objektu pro vytváření `<img>` značky na stránce a přijímá několik vstupních parametrů včetně id, adresy url a alternativní text obrázku značky. Logika se pak přidá do funkce pro vracení dokončené `<img>` značky se zadanými informacemi. Vlastní HtmlHelper použije se na stránce Ukázky obrázek. Nakonec je vlastní HtmlHelper rozšířen, aby zahrnoval několik konstruktor přepsání, které poskytují flexibilitu pro více snadno vytvářet různé `<img>` značky.

[&#9654;Podívejte se na video (18 minut)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> [Předchozí](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [další](how-do-i-work-with-model-binders-in-an-mvc-application.md)
