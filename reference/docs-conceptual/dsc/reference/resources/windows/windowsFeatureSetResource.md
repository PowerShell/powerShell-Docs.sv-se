---
ms.date: 07/16/2020
ms.topic: reference
title: DSC WindowsFeatureSet-resurs
description: DSC WindowsFeatureSet-resurs
ms.openlocfilehash: 327c5e907e9b100f42b6a15684f8b131c1f20a41
ms.sourcegitcommit: 196c7f8cd24560cac70c88acc89909f17a86aea9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/31/2020
ms.locfileid: "93143083"
---
# <a name="dsc-windowsfeatureset-resource"></a>DSC WindowsFeatureSet-resurs

> Gäller för: Windows PowerShell 5. x

**WindowsFeatureSet** -resursen i Windows PowerShell Desired State Configuration (DSC) tillhandahåller en mekanism för att se till att roller och funktioner läggs till eller tas bort på en målnod. Den här resursen är en [sammansatt resurs](../../../resources/authoringResourceComposite.md) som anropar [WindowsFeature-resursen](windowsfeatureResource.md) för varje funktion som anges i egenskapen **Name** .

Använd den här resursen när du vill konfigurera ett antal Windows-funktioner till samma tillstånd.

[!INCLUDE [Updated DSC Resources](../../../../../includes/dsc-resources.md)]

## <a name="syntax"></a>Syntax

```Syntax
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [Boolean] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

## <a name="properties"></a>Egenskaper

|  Egenskap  |  Beskrivning   |
|---|---|
|Namn |Namnen på de roller eller funktioner som du vill se läggs till eller tas bort. Detta är samma som egenskapen **Name** för cmdleten [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) och inte visnings namnet för rollerna eller funktionerna. |
|Källa |Anger platsen för den käll fil som ska användas för installation, om det behövs. |
|IncludeAllSubFeature |Ange den här egenskapen till `$true` att inkludera alla nödvändiga underfunktioner med de funktioner som du anger med egenskapen **Name** . |
|Autentiseringsuppgift |De autentiseringsuppgifter som ska användas för att lägga till eller ta bort roller och funktioner. |
|LogPath |Sökvägen till logg filen där du vill att resurs leverantören ska logga åtgärden. |

## <a name="common-properties"></a>Gemensamma egenskaper

|Egenskap |Beskrivning |
|---|---|
|DependsOn |Anger att konfigurationen av en annan resurs måste köras innan den här resursen har kon figurer ATS. Exempel: om ID: t för skript blocket för resurs konfigurationen som du vill köra först är ResourceName och dess typ är ResourceType, är syntaxen för att använda den här egenskapen `DependsOn = "[ResourceType]ResourceName"` . |
|Kontrol |Anger om roller eller funktioner läggs till. Om du vill kontrol lera att rollerna eller funktionerna har lagts till ställer du in den här egenskapen som **tillgänglig** . För att säkerställa att rollerna eller funktionerna tas bort ställer du in egenskapen på **saknas** . Standardvärdet finns **.** |
|PsDscRunAsCredential |Anger autentiseringsuppgifter för att köra hela resursen som. |

> [!NOTE]
> Den gemensamma egenskapen **PsDscRunAsCredential** har lagts till i WMF 5,0 för att tillåta körning av DSC-resurser i kontexten för andra autentiseringsuppgifter. Mer information finns i [använda autentiseringsuppgifter med DSC-resurser](../../../configurations/runasuser.md).

## <a name="example"></a>Exempel

Följande konfiguration säkerställer att funktionerna för **webb server** (IIS) och **SMTP-servern** och alla underfunktioner i respektive är installerade.

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        }
    }
}
```
