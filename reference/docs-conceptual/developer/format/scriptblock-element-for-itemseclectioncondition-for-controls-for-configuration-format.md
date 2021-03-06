---
ms.date: 09/13/2016
ms.topic: reference
title: ScriptBlock-element för ItemSeclectionCondition för Controls för Configuration (format)
description: ScriptBlock-element för ItemSeclectionCondition för Controls för Configuration (format)
ms.openlocfilehash: 853130da4489e571d7f4026a8d65d029d1889f9b
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/10/2020
ms.locfileid: "92665221"
---
# <a name="scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format"></a>ScriptBlock-element för ItemSeclectionCondition för Controls för Configuration (format)

Anger det skript som utlöser villkoret. När det här skriptet utvärderas `true` , uppfylls villkoret och kontrollen används. Det här elementet används när du definierar en gemensam kontroll som kan användas av alla vyer i format filen.

Konfigurations element (format) styr element i konfigurations-(format)-kontroll element för Controls (format) CustomControl-element för Control för Configuration (format) CustomEntries-element för CustomControl för Configuration (format) CustomEntry-element för CustomControl för kontroller för konfiguration (format) CustomItem-element för CustomEntry for Controls for Configuration ExpressionBinding element for CustomItem for Controls for Configuration (format) ItemSelectionCondition element for ExpressionBinding for Controls for Configuration (format) script block element for ItemSelectionCondition for Controls for Configuration (format)

## <a name="syntax"></a>Syntax

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a>Attribut och element

I följande avsnitt beskrivs attribut, underordnade element och `ScriptBlock` elementets överordnade element.

### <a name="attributes"></a>Attribut

Inga.

### <a name="child-elements"></a>Underordnade element

Inga.

### <a name="parent-elements"></a>Överordnade element

|Element|Beskrivning|
|-------------|-----------------|
|[ItemSelectionCondition-element för ExpressionBinding för Controls för Configuration (format)](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)|Definierar det villkor som måste finnas för att den här kontrollen ska kunna användas.|

## <a name="text-value"></a>Textvärde

Ange det skript som utvärderas.

## <a name="remarks"></a>Kommentarer

Om det här elementet används kan du inte ange elementet [PropertyName](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md) när du definierar urvals villkoret.

## <a name="see-also"></a>Se även

[PropertyName-element för ItemSeclectionCondition för Controls för Configuration (format)](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)

[ItemSelectionCondition-element för ExpressionBinding för Controls för Configuration (format)](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)

[Skriva en PowerShell-formateringsfil](./writing-a-powershell-formatting-file.md)
