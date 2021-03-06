---
ms.date: 07/17/2020
ms.topic: reference
title: DSC för Linux nxPackage-resurs
description: DSC för Linux nxPackage-resurs
ms.openlocfilehash: b84c7963297e8a88e729cd67611245b017c27fb7
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/27/2020
ms.locfileid: "92648837"
---
# <a name="dsc-for-linux-nxpackage-resource"></a>DSC för Linux nxPackage-resurs

**NxPackage** -resursen i PowerShell Desired State Configuration (DSC) tillhandahåller en mekanism för att hantera paket på en Linux-nod.

## <a name="syntax"></a>Syntax

```Syntax
nxPackage <string> #ResourceName
{
    Name = <string>
    [ PackageManager = <string> { Yum | Apt | Zypper } ]
    [ PackageGroup = <bool>]
    [ Arguments = <string> ]
    [ ReturnCode = <uint32> ]
    [ FilePath = <string> ]
    [ DependsOn = <string[]> ]
    [ Ensure = <string> { Absent | Present }  ]
}
```

## <a name="properties"></a>Egenskaper

|Egenskap |Beskrivning |
|---|---|
|Namn |Namnet på det paket som du vill säkerställa ett speciellt tillstånd för. |
|PackageManager |De värden som stöds är **yum** , **apt** och **zypper** . Anger vilken paket hanterare som ska användas för att installera paket. Om **sökväg anges används** den angivna sökvägen för att installera paketet. Annars kommer en paket hanterare att användas för att installera paketet från en förkonfigurerad lagrings plats. Om varken **PackageManager** eller **sökväg** anges används standard paket hanteraren för systemet. |
|PackageGroup |Om `$true` **namnet** förväntas vara namnet på en paket grupp som ska användas med en **PackageManager** . **PackageGroup** är inte giltig vid en **fil Sök väg** . |
|Argument |En sträng med argument som skickas till paketet exakt som det anges. |
|ReturnCode |Den förväntade retur koden. Om den faktiska retur koden inte matchar det förväntade värdet här, returnerar konfigurationen ett fel. |
|FilePath |Sökvägen till filen där paketet finns. |

## <a name="common-properties"></a>Gemensamma egenskaper

|Egenskap |Beskrivning |
|---|---|
|DependsOn |Anger att konfigurationen av en annan resurs måste köras innan den här resursen har kon figurer ATS. Exempel: om ID: t för skript blocket för resurs konfigurationen som du vill köra först är ResourceName och dess typ är ResourceType, är syntaxen för att använda den här egenskapen `DependsOn = "[ResourceType]ResourceName"` . |
|Kontrol |Avgör om det finns ett paket som ska kontrol leras. Ange att den här egenskapen **finns** för att se till att paketet finns. Ange det som **frånvarande** för att säkerställa att paketet inte finns. Standardvärdet finns **.** |

## <a name="example"></a>Exempel

I följande exempel ser du till att paketet med namnet "httpd" är installerat på en Linux-dator med hjälp av paket hanteraren "yum".

```powershell
Import-DSCResource -Module nx

Node $node
{
    nxPackage httpd
    {
        Name = "httpd"
        Ensure = "Present"
        PackageManager = "Yum"
    }
}
```
