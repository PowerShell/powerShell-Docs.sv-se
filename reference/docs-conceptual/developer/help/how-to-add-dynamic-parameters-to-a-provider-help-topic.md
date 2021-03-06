---
ms.date: 09/13/2016
ms.topic: reference
title: Lägga till dynamiska parametrar i ett hjälpavsnitt för providers
description: Lägga till dynamiska parametrar i ett hjälpavsnitt för providers
ms.openlocfilehash: 9542538cfacf5fb293ca8d1350b80fb250c71ac6
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/10/2020
ms.locfileid: "92649636"
---
# <a name="how-to-add-dynamic-parameters-to-a-provider-help-topic"></a>Lägga till dynamiska parametrar i ett hjälpavsnitt för providers

I det här avsnittet beskrivs hur du fyller i avsnittet **dynamiska parametrar** i en providers hjälp avsnitt.

*Dynamiska parametrar* är parametrar för en cmdlet eller funktion som endast är tillgängliga under angivna villkor.

De dynamiska parametrar som dokumenteras i ett hjälp avsnitt om providern är de dynamiska parametrar som providern lägger till i cmdleten eller funktionen när-cmdleten eller-funktionen används i leverantörs enheten.

Dynamiska parametrar kan också dokumenteras i anpassad cmdlet-hjälp för en provider. När du skriver både hjälpen för Provider och anpassad cmdlet-hjälp för en provider, inkluderar du den dynamiska parameter dokumentationen i båda dokumenten.

Om en provider inte implementerar några dynamiska parametrar innehåller leverantörens hjälp avsnitt ett tomt `DynamicParameters` element.

### <a name="to-add-dynamic-parameters"></a>Lägga till dynamiska parametrar

1. `<AssemblyName>.dll-help.xml` `providerHelp` Lägg till ett-element i-filen i-elementet `DynamicParameters` . `DynamicParameters`Elementet ska visas efter `Tasks` elementet och före `RelatedLinks` elementet.

   Exempel:

    ```xml
    <providerHelp>
        <Tasks>
        </Tasks>
        <DynamicParameters>
        </DynamicParameters>
        <RelatedLinks>
        </RelatedLinks>
    </providerHelp>
    ```

   Om providern inte implementerar några dynamiska parametrar `DynamicParameters` kan elementet vara tomt.

1. I `DynamicParameters` elementet lägger du till ett-element för varje dynamisk parameter `DynamicParameter` .

   Exempel:

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
        </DynamicParameter>
    </DynamicParameters>
    ```

1. I varje `DynamicParameter` element lägger du till ett `Name` och- `CmdletSupported` element.

   - Namn – anger parameter namnet
   - CmdletSupported – anger cmdletarna där parametern är giltig. Ange en kommaavgränsad lista med cmdlet-namn.

   Till exempel innehåller följande XML-filer den `Encoding` dynamiska parametern som Windows PowerShell-filleverantören lägger till `Add-Content` i `Get-Content` `Set-Content` cmdletarna.

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
            <Name> Encoding </Name>
            <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
    </DynamicParameters>

    ```

1. I varje `DynamicParameter` element lägger du till ett- `Type` element. `Type`Elementet är en behållare för det `Name` element som innehåller .net-typen för den dynamiska parameterns värde.

   Till exempel visar följande XML att .NET-typen för den `Encoding` dynamiska parametern är [FileSystemCmdletProviderEncoding](/dotnet/api/microsoft.powershell.commands.filesystemcmdletproviderencoding) -uppräkningen.

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
            <Name> Encoding </Name>
            <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
            <Type>
                <Name> Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding </Name>
            <Type>
    ...
    </DynamicParameters>
    ```

1. Lägg till `Description` elementet, som innehåller en kort beskrivning av den dynamiska parametern. När du skriver beskrivningen använder du rikt linjerna för alla cmdlet-parametrar i [så här lägger du till parameter information](./how-to-add-parameter-information.md).

   Till exempel innehåller följande XML en beskrivning av den `Encoding` dynamiska parametern.

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
            <Name> Encoding </Name>
            <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
            <Type>
                <Name> Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding </Name>
            <Type>
            <Description> Specifies the encoding of the output file that contains the content. </Description>
    ...
    </DynamicParameters>
    ```

1. Lägg till `PossibleValues` elementet och dess underordnade element. Tillsammans beskriver de här elementen värdena för den dynamiska parametern. Det här elementet är utformat för uppräknade värden. Om den dynamiska parametern inte tar ett värde, t. ex. är fallet med en växlings parameter, eller om värdena inte kan räknas upp, lägger du till ett tomt `PossibleValues` element.

   I följande tabell visas och beskrivs `PossibleValues` elementet och dess underordnade element.

   - PossibleValues – det här elementet är en behållare. De underordnade elementen beskrivs nedan. Lägg till ett `PossibleValues` element i varje leverantörs hjälp avsnitt. Elementet kan vara tomt.
   - PossibleValue – det här elementet är en behållare. De underordnade elementen beskrivs nedan. Lägg till ett- `PossibleValue` element för varje värde för den dynamiska parametern.
   - Value-anger värde namnet.
   - Beskrivning – Det här elementet innehåller ett- `Para` element. Texten i `Para` elementet beskriver det värde som namnges i `Value` elementet.

   I följande XML visas till exempel ett `PossibleValue` element i den `Encoding` dynamiska parametern.

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
    ...
            <Description> Specifies the encoding of the output file that contains the content. </Description>
            <PossibleValues>
                <PossibleValue>
                    <Value> ASCII </Value>
                    <Description>
                        <para> Uses the encoding for the ASCII (7-bit) character set. </para>
                    </Description>
                </PossibleValue>
    ...
            </PossibleValues>
    </DynamicParameters>
    ```

## <a name="example"></a>Exempel

I följande exempel visas `DynamicParameters` elementet i den `Encoding` dynamiska parametern.

```xml
<DynamicParameters/>
    <DynamicParameter>
        <Name> Encoding </Name>
        <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
        <Type>
            <Name> Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding </Name>
        <Type>
        <Description> Specifies the encoding of the output file that contains the content. </Description>
        <PossibleValues>
            <PossibleValue>
                <Value> ASCII </Value>
                <Description>
                    <para> Uses the encoding for the ASCII (7-bit) character set. </para>
                </Description>
            </PossibleValue>
            <PossibleValue>
                <Value> Unicode </Value>
                <Description>
                    <para> Encodes in UTF-16 format using the little-endian byte order. </para>
                </Description>
            </PossibleValue>
        </PossibleValues>
</DynamicParameters>
```
