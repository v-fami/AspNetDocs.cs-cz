---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: Použití postbacků s ovládacím prvkem ReorderList (VB) | Dokumentace Microsoftu
author: wenz
description: Ovládacím prvkem ReorderList ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení. Pokaždé, když je pořadí v seznamu změníte, po...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: e2ab485d276d62518b6e7317bd76121f18d27ba8
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124725"
---
# <a name="using-postbacks-with-reorderlist-vb"></a>Použití postbacků s ovládacím prvkem ReorderList (VB)

by [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)

> Ovládacím prvkem ReorderList ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení. Pokaždé, když je pořadí v seznamu změníte, zpětné volání informuje server změny.

## <a name="overview"></a>Přehled

`ReorderList` Ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení. Pokaždé, když je pořadí v seznamu změníte, zpětné volání informuje server změny.

## <a name="steps"></a>Kroky

Existuje několik datových zdrojů pro `ReorderList` ovládacího prvku. Jeden má používat `XmlDataSource` ovládacího prvku:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

Vázat tento XML tak, aby `ReorderList` postbacků ovládacího prvku a povolit, následující atributy musí být nastavena:

- `DataSourceID`: ID zdroje dat
- `SortOrderField`: Vlastnost, která má řadit podle
- `AllowReorder`: Jestli se má povolit uživatelům změnit uspořádání seznamu elementů
- `PostBackOnReorder`: Jestli chcete vytvořit zpětné volání pokaždé, když je změnit jejich uspořádání seznamu

Tady je odpovídající značky ovládacího prvku:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

V rámci `ReorderList` ovládacího prvku, konkrétní data ze zdroje dat, může být vázaný pomocí `Eval()` metody:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

Na libovolné pozici na stránce popisek bude obsahovat informace, kdy poslední změny pořadí došlo k chybě:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

Tento popisek je vyplněna text v kódu na straně serveru, zpracování zpětného volání:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

Nakonec, aby bylo možné aktivovat funkce technologie ASP.NET AJAX a Control Toolkit `ScriptManager` ovládací prvek je třeba umístit na stránce:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]

[![Každá změna uspořádání aktivuje zpětné volání](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)

Každá změna uspořádání aktivuje zpětné volání ([kliknutím ji zobrazíte obrázek v plné velikosti](using-postbacks-with-reorderlist-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Předchozí](drag-and-drop-via-reorderlist-cs.md)
> [další](drag-and-drop-via-reorderlist-vb.md)
