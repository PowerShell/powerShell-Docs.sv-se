---
ms.date: 09/13/2016
ms.topic: reference
title: CustomEntry-element för CustomEntries för CustomControl för View (format)
description: CustomEntry-element för CustomEntries för CustomControl för View (format)
ms.openlocfilehash: ff481f13e6f16267bdda4c3053faebc96d9a6d3a
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/10/2020
ms.locfileid: "92646057"
---
# <a name="customentry-element-for-customentries-for-customcontrol-for-view-format"></a>CustomEntry-element för CustomEntries för CustomControl för View (format)

Innehåller en definition av den anpassade kontrollen.

Konfigurations element (format) ViewDefinitions element (format) View element (format) CustomControl element (format) CustomEntries-element för CustomControl för View (format) CustomEntry-element för CustomEntries för vy (format)

## <a name="syntax"></a>Syntax

```xml
<CustomEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <CustomItem>...</CustomItem>
</CustomEntry>
```

## <a name="attributes-and-elements"></a>Attribut och element

I följande avsnitt beskrivs attribut, underordnade element och `CustomEntry` elementets överordnade element. Du måste ange de objekt som ska visas av definitionen.

### <a name="attributes"></a>Attribut

Inga.

### <a name="child-elements"></a>Underordnade element

|Element|Beskrivning|
|-------------|-----------------|
|[EntrySelectedBy-element för CustomEntry för vy (format)](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)|Valfritt element.<br /><br /> Definierar de .NET-typer som använder definitionen av den anpassade kontrollen eller det villkor som måste finnas för att den här definitionen ska användas.|
|[CustomItem-element för CustomEntry för vy (format)](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)|Definierar en kontroll för definitionen av den anpassade kontrollen.|

### <a name="parent-elements"></a>Överordnade element

|Element|Beskrivning|
|-------------|-----------------|
|[CustomEntries-element för CustomControl för View (format)](./customentries-element-for-customcontrol-for-view-format.md)|Innehåller definitionerna för vyn anpassad kontroll. Vyn anpassad kontroll måste ange en eller flera definitioner.|

## <a name="remarks"></a>Kommentarer

I de flesta fall krävs bara en definition för varje anpassad kontroll, men det är möjligt att ha flera definitioner om du vill använda samma vy för att visa olika .NET-objekt. I dessa fall kan du ange en separat definition för varje objekt eller uppsättning objekt.

## <a name="see-also"></a>Se även

[CustomControl-element för View (format)](./customcontrol-element-for-view-format.md)

[CustomItem-element för CustomEntry för vy (format)](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)

[EntrySelectedBy-element för CustomEntry för vy (format)](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)

[Skriva en PowerShell-formateringsfil](./writing-a-powershell-formatting-file.md)
