---
ms.date: 09/13/2016
ms.topic: reference
title: WideControl-element (format)
description: WideControl-element (format)
ms.openlocfilehash: f88e1ce18f87e5e47de473298b3ecf070b71c192
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/10/2020
ms.locfileid: "92651274"
---
# <a name="widecontrol-element-format"></a>WideControl-element (format)

Definierar ett brett List format (enskilt värde) för vyn. I den här vyn visas ett enskilt egenskaps värde eller skript värde för varje objekt.

Konfigurations element (format) ViewDefinitions element (format) Visa element (format) WideControl-element (format)

## <a name="syntax"></a>Syntax

```xml
<WideControl>
  <AutoSize/>
  <ColumnNumber>PositiveInteger</ColumnNumber>
  <WideEntries>...</WideEntries>
</WideControl>
```

## <a name="attributes-and-elements"></a>Attribut och element

I följande avsnitt beskrivs attributen, underordnade element och `WideControl` elementets överordnade element. Du kan inte ange `AutoSize` `ColumnNumber` elementen och på samma tidpunkt.

### <a name="attributes"></a>Attribut

Inga.

### <a name="child-elements"></a>Underordnade element

|Element|Beskrivning|
|-------------|-----------------|
|[AutoSize-element för WideControl (format)](./autosize-element-for-widecontrol-format.md)|Valfritt element.<br /><br /> Anger om kolumn storleken och antalet kolumner justeras baserat på data storleken.|
|[ColumnNumber-element för WideControl (format)](./columnnumber-element-for-widecontrol-format.md)|Valfritt element.<br /><br /> Anger antalet kolumner som visas i den bred vyn.|
|[WideEntries-element (format)](./wideentries-element-for-widecontrol-format.md)|Nödvändigt element.<br /><br /> Innehåller definitionerna för den breda vyn.|

### <a name="parent-elements"></a>Överordnade element

|Element|Beskrivning|
|-------------|-----------------|
|[View-element (format)](./view-element-format.md)|Definierar en vy som används för att visa ett eller flera .NET-objekt.|

## <a name="remarks"></a>Kommentarer

När du definierar en bred vy kan du lägga till `AutoSize` elementet eller, `ColumnNumber` men du kan inte lägga till båda.

I de flesta fall krävs bara en definition för varje bred vy, men det är möjligt att ha flera definitioner om du vill använda samma vy för att visa olika .NET-objekt. I dessa fall kan du ange en separat definition för varje objekt eller uppsättning objekt.

Mer information om komponenterna i en bred vy finns i [wide View-komponenter](./creating-a-wide-view.md).

## <a name="example"></a>Exempel

I följande exempel visas ett- `WideControl` element som används för att visa en egenskap för objektet [system. Diagnostics. process](/dotnet/api/System.Diagnostics.Process) .

```xml
<View>
  <Name>process</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <WideControl>
    <WideEntries>...</WideEntries>
  </WideControl>
</View>
```

Ett fullständigt exempel på en bred vy finns i [wide View (grundläggande)](./wide-view-basic.md).

## <a name="see-also"></a>Se även

[AutoSize-element för WideControl (format)](./autosize-element-for-widecontrol-format.md)

[ColumnNumber-element för WideControl (format)](./columnnumber-element-for-widecontrol-format.md)

[View-element (format)](./view-element-format.md)

[WideEntries-element (format)](./wideentries-element-for-widecontrol-format.md)

[Bred vy (grundläggande)](./wide-view-basic.md)

[Skapa en bred vy](./creating-a-wide-view.md)

[Skriva en PowerShell-formateringsfil](./writing-a-powershell-formatting-file.md)
