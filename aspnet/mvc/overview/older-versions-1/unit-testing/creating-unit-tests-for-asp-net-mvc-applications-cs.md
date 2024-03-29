---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: Vytváření testů jednotek pro aplikace ASP.NET MVC (C#) | Dokumentace Microsoftu
author: StephenWalther
description: Zjistěte, jak vytvářet testy částí pro akce kontroleru. V tomto kurzu Stephen Walther ukazuje, jak otestovat, jestli akce kontroleru vrátí sloupce části...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 633e28a100937c5d40d62fe5cc151e613171cc8f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65126885"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a>Vytváření testů jednotek pro aplikace ASP.NET MVC (C#)

podle [Stephen Walther](https://github.com/StephenWalther)

[Stáhnout PDF](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> Zjistěte, jak vytvářet testy částí pro akce kontroleru. V tomto kurzu Stephen Walther ukazuje, jak otestovat, jestli akce kontroleru vrátí konkrétní zobrazení, vrátí konkrétní sady dat nebo vrátí jiný typ výsledku akce.

Cílem tohoto kurzu je předvést, jak psát testy jednotek pro kontrolery v ASP.NET MVC aplikace. Pojednává o vytváření tří různých typů testů jednotek. Zjistíte, jak prohlížeč vrácené akcí kontroleru testů, jak testovat zobrazení dat vrácených akce kontroleru a jak otestovat, jestli jedna akce kontroleru vás přesměruje na druhou akci kontroleru.

## <a name="creating-the-controller-under-test"></a>Vytvoření Kontroleru v rámci testu

Začněme vytvořením kontroleru, který chceme otestovat. Kontroler, s názvem `ProductController`, je obsažen v informacích 1.

**Výpis 1 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

`ProductController` Obsahuje dvě metody akce s názvem `Index()` a `Details()`. Obě metody akce vracejí zobrazení. Všimněte si, že `Details()` akce přijme parametr s názvem ID.

## <a name="testing-the-view-returned-by-a-controller"></a>Testování zobrazení vrácený Kontroleru

Představte si, že chceme otestovat, zda je či není `ProductController` vrátí z druhého zobrazení. Chceme, abyste měli jistotu, že `ProductController.Details()` akce je volána, vrátí se zobrazení podrobností. Testovací třídy v informacích 2 obsahuje testování částí pro testování zobrazení vrácených `ProductController.Details()` akce.

**Výpis 2 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

Třída v informacích 2 zahrnuje testovací metodu s názvem `TestDetailsView()`. Tato metoda obsahuje tři řádky kódu. První řádek kódu vytvoří novou instanci třídy `ProductController` třídy. Druhý řádek kódu vyvolá kontroleru `Details()` metody akce. Nakonec poslední řádek kódu kontroly, zda zobrazení vrácené `Details()` akce je zobrazení podrobností.

`ViewResult.ViewName` Vlastnost představuje název zobrazení, které vrácený řadič. Jeden velký upozornění o testování této vlastnosti. Existují dva způsoby, že řadič lze vrátit zobrazení. Kontroler explicitně lze vrátit zobrazení takto:

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

Název zobrazení, případně lze odvodit z název akce kontroleru takto:

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

Tato akce kontroleru vrátí také zobrazení s názvem `Details`. Název zobrazení je však odvozen z názvu akce. Pokud chcete zobrazit název testu, pak musíte explicitně vrátit název zobrazení z akce kontroleru.

Můžete spustit testování částí v informacích 2 zadáním kombinace kláves **Ctrl-R, A** nebo kliknutím **spustit všechny testy v řešení** tlačítko (viz obrázek 1). Pokud je test úspěšný, zobrazí se vám okně Výsledky testu na obrázku 2.

[![Spustit všechny testy v řešení](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)

**Obrázek 01**: Spustit všechny testy v řešení ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))

[![Úspěch!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)

**Obrázek 02**: Úspěch! ([Kliknutím ji zobrazíte obrázek v plné velikosti](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))

## <a name="testing-the-view-data-returned-by-a-controller"></a>Testování zobrazení dat vrácených Kontroleru

Kontroler MVC předá data k zobrazení pomocí nástroje s názvem *`View Data`*. Představte si například, že chcete zobrazit podrobnosti pro konkrétní produkt při vyvolání `ProductController Details()` akce. V takovém případě můžete vytvořit instanci `Product` třídy (definované v modelu) a předejte instanci `Details` zobrazení s využitím `View Data`.

Upravené `ProductController` výpis 3 zahrnuje aktualizovanou `Details()` akci, která vrací produktu.

**Výpis 3 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

Nejprve je potřeba `Details()` akce vytvoří novou instanci třídy `Product` třídu, která představuje přenosný počítač. Další, instance `Product` třídy je předán jako druhý parametr `View()` metody.

Můžete napsat jednotkové testy k ověření, zda je očekávaná data obsažená v zobrazení data. Testování jednotek v testech výpis 4, zda produktu představující přenosný počítač je vrácena při volání `ProductController Details()` metody akce.

**Část 4 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

V informacích 4 `TestDetailsView()` metoda otestováním zobrazení dat vrácených volání `Details()` metody. `ViewData` Vystavena jako vlastnost na `ViewResult` vrátil vyvoláním `Details()` metody. `ViewData.Model` Vlastnost obsahuje produkt předána do zobrazení. Test jednoduše ověří, zda produktu obsažené v zobrazení dat má název přenosném počítači.

## <a name="testing-the-action-result-returned-by-a-controller"></a>Testování výsledek akce vrácené Kontroleru

Složitější akce kontroleru může vrátit různé typy výsledků akcí v závislosti na hodnoty parametrů předaných pracovnímu akce kontroleru. Akce kontroleru vrátit různé typy výsledků akcí, včetně `ViewResult`, `RedirectToRouteResult`, nebo `JsonResult`.

Například upravené `Details()` vrátí v informacích 5 akci `Details` zobrazit při předání platný kód product Id akce. Pokud předáte neplatné Id produktu – Id s hodnotou, menší než 1 – budete přesměrováni `Index()` akce.

**Výpis 5 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

Můžete otestovat chování `Details()` akce s testováním částí v informacích 6. Testování částí v informacích 6 ověřuje, že budete přesměrováni na `Index` zobrazovat, když se Id s hodnotou -1 je předána `Details()` metody.

**Výpis 6 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

Při volání `RedirectToAction()` metoda akce kontroleru, akce kontroleru vrátí `RedirectToRouteResult`. Test zkontroluje, jestli `RedirectToRouteResult` přesměruje uživatele na kontroler akce s názvem `Index`.

## <a name="summary"></a>Souhrn

V tomto kurzu jste zjistili, jak vytvářet testy částí pro akce řadiče MVC. Nejdřív jste zjistili, jak ověřit, jestli je akce kontroleru vrácený z druhého zobrazení. Naučili jste se použít `ViewResult.ViewName` vlastnost ověřte název zobrazení.

Dále jsme se zaměřili na tom, jak můžete otestovat obsah `View Data`. Jste zjistili, jak zkontrolovat, zda byl vrácen správný produkt v `View Data` po volání metody akce kontroleru.

Nakonec jsme zmínili, jak můžete zkontrolovat, jestli se z akce kontroleru vrátí různé typy výsledků akcí. Jste zjistili, jak chcete otestovat, jestli kontroler vrací `ViewResult` nebo `RedirectToRouteResult`.

> [!div class="step-by-step"]
> [Next](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
