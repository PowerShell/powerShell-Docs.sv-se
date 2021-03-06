---
ms.date: 09/13/2016
ms.topic: reference
title: TableColumnHeader-element (format)
description: TableColumnHeader-element (format)
ms.openlocfilehash: 30368512875b7c5c4cf3c686f3d09540dea1bd26
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/10/2020
ms.locfileid: "92651518"
---
# <a name="tablecolumnheader-element-format"></a>TableColumnHeader-element (format)

Definierar etiketten, bredden på kolumnen och justeringen av etiketten för en kolumn i tabellen.

Konfigurations element (format) ViewDefinitions element (format) View-element (format) TableControl element (format) TableHeaders-element för TableControl (format) TableColumnHeader-element för TableHeaders (format)

## <a name="syntax"></a>Syntax

```xml
<TableColumnHeader>
  <Label>DisplayedLabel</Label>
  <Width>NumberOfCharacters</Width>
  <Alignment>Left, Right, or Centered</Alignment>
</TableColumnHeader>
```

## <a name="attributes-and-elements"></a>Attribut och element

I följande avsnitt beskrivs attribut, underordnade element och `TableColumnHeader` elementets överordnade element.

### <a name="attributes"></a>Attribut

Inga.

### <a name="child-elements"></a>Underordnade element

|Element|Beskrivning|
|-------------|-----------------|
|[Etikett element för TableColumnHeader för TableControl (format)](./label-element-for-tablecolumnheader-for-tablecontrol-format.md)|Valfritt element.<br /><br /> Definierar etiketten som visas överst i kolumnen. Om ingen etikett anges används namnet på den egenskap vars värde visas i raderna.|
|[Width-element för TableColumnHeader för TableControl (format)](./width-element-for-tablecolumnheader-for-tablecontrol-format.md)|Nödvändigt element.<br /><br /> Anger bredden (i tecken) för kolumnen.|
|[Alignment-element för TableColumnHeader för TableControl (format)](./alignment-element-for-tablecolumnheader-for-tablecontrol-format.md)|Valfritt element.<br /><br /> Anger hur kolumnens etikett visas. Om ingen justering anges justeras etiketten till vänster.|

### <a name="parent-elements"></a>Överordnade element

|Element|Beskrivning|
|-------------|-----------------|
|[TableHeaders-element (format)](./tableheaders-element-format.md)|Definierar kolumnerna i en tabellvy.|

## <a name="remarks"></a>Kommentarer

Ange ett sidhuvud för varje kolumn i tabellen. Kolumnerna visas i den ordning som `TableColumnHeader` elementen definieras i.

En tabell måste ha samma antal `TableColumnHeader` element som `TableRowEntry` element. Kolumn rubriken definierar hur texten överst i tabellen visas. Rad posterna definierar vilka data som visas i raderna i tabellen.

Mer information om komponenterna i en tabellvy finns i [tabellvy](./creating-a-table-view.md).

## <a name="example"></a>Exempel

I följande exempel visas två `TableColumnHeader` element. Det första elementet definierar en kolumn vars etikett är "kolumn 1", har en bredd på 16 tecken och vars etikett är justerad till vänster. Det andra elementet definierar en kolumn vars etikett är "kolumn 2", har en bredd på 10 tecken och vars etikett centreras i kolumnen.

```xml
<TableHeaders>
  <TableColumnHeader>
    <Label>Column 1</Label)
    <Width>16</Width>
    <Alignment>Left</Alignment>
  </TableColumnHeader>
    <TableColumnHeader>
    <Label>Column 2</Label)
    <Width>10</Width>
    <Alignment>Centered</Alignment>
  </TableColumnHeader>
</TableHeaders>
```

## <a name="see-also"></a>Se även

[Alignment-element för TableColumnHeader för TableControl (format)](./alignment-element-for-tablecolumnheader-for-tablecontrol-format.md)

[Skapa en tabellvy](./creating-a-table-view.md)

[Label-element för TableColumnHeader för TableControl (format)](./label-element-for-tablecolumnheader-for-tablecontrol-format.md)

[TableHeaders-element för TableControl (format)](./tableheaders-element-format.md)

[Bredd för TableColumnHeader för TableControl-element (format)](./width-element-for-tablecolumnheader-for-tablecontrol-format.md)

[Skriva en PowerShell-formateringsfil](./writing-a-powershell-formatting-file.md)
