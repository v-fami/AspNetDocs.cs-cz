---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: Postupné provedení několika animací ve stejnou dobu (VB) | Dokumentace Microsoftu
author: wenz
description: Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Umožňuje spustit severa...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: 02eb078a4fb8fddbbac18e4631214f354388cc2f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65133414"
---
# <a name="executing-several-animations-at-the-same-time-vb"></a>Postupné provedení několika animací ve stejnou dobu (VB)

by [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)

> Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. To umožňuje spuštění několika animací paralelní způsobem.

## <a name="overview"></a>Přehled

Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. To umožňuje spuštění několika animací paralelní způsobem.

## <a name="steps"></a>Kroky

Za prvé, zahrnout `ScriptManager` na stránce; potom technologie ASP.NET AJAX je načíst knihovnu, což umožňuje použití Control Toolkit:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

Animace se použijí pro panel text, který vypadá takto:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

V přidružené třídy šablony stylů CSS pro panel definovat barvu pozadí nice a také nastavit Pevná šířka panelu:

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

Pak přidejte `AnimationExtender` na stránku, poskytování `ID`, `TargetControlID` atribut a povinný údaj `runat="server"`:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

V rámci `<Animations>` uzlu, použijte `<OnLoad>` ke spuštění animací, jakmile úplným načtením stránky. Obecně platí `<OnLoad>` přijímá pouze jeden animace. Animace framework umožňuje připojit k několika animací do jednoho pomocí `<Parallel>` elementu. Všechny animace v rámci `<Parallel>` jsou spouštěny ve stejnou dobu.

Tady je možné značky `AnimationExtender` ovládacího prvku, mizení a změnu velikosti panelu ve stejnou dobu:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

A skutečně: při spuštění tohoto skriptu na panelu se zobrazí poté změní (více než tripling šířku a výšku halving) a setmívá ve stejnou dobu.

[![Na panelu je mizení a změna velikosti (včetně jeho obsahu díky prohlížeče vykreslovací modul)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)

Na panelu je mizení a změna velikosti (včetně jeho obsahu díky prohlížeče vykreslovací modul) ([kliknutím ji zobrazíte obrázek v plné velikosti](executing-several-animations-at-the-same-time-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Předchozí](adding-animation-to-a-control-vb.md)
> [další](executing-several-animations-after-each-other-vb.md)
