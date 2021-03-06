---
ms.date: 06/12/2017
title: Felkorrigeringar i WMF 5.1
description: Den här artikeln innehåller de fel som har åtgärd ATS i lanseringen av WMF 5,1.
ms.openlocfilehash: 2673860852ecd6e0b6582f6f69076f8c463eeccc
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/27/2020
ms.locfileid: "92660769"
---
# <a name="bug-fixes-in-wmf-51"></a>Felkorrigeringar i WMF 5.1

## <a name="bug-fixes"></a>Felkorrigeringar

Följande viktiga buggar korrigeras i WMF 5,1:

### <a name="module-auto-discovery-fully-honors-psmodulepath"></a>Automatisk identifiering av modulen PSModulePath

Automatisk identifiering av modul (moduler som läses in automatiskt utan en explicit Import-Module när ett kommando anropas) introducerades i WMF 3. När den introducerades kontrollerar PowerShell för kommandon i `$PSHome\Modules` innan du använder `$env:PSModulePath` .

WMF 5,1 ändrar det här beteendet för att respektera `$env:PSModulePath` fullständigt. Detta gör att en användardefinierad modul som definierar kommandon som tillhandahålls av PowerShell (t. ex. `Get-ChildItem` ) automatiskt läses in och som åsidosätter det inbyggda kommandot.

### <a name="file-redirection-no-longer-hard-codes--encoding-unicode"></a>Omdirigering av fil är inte längre hårdkodade Unicode-kodning

I alla tidigare versioner av PowerShell var det omöjligt att kontrol lera fil kodningen som används av operatorn för fil omdirigering.

Från och med WMF 5,1 kan du nu ändra fil kodningen för omdirigering genom att ställa in `$PSDefaultParameterValues` :

```powershell
$PSDefaultParameterValues["Out-File:Encoding"] = "Ascii"
```

### <a name="fixed-a-regression-in-accessing-members-of-systemreflectiontypeinfo"></a>Fast en regression vid åtkomst till medlemmar i system. Reflection. TypeInfo

En regression som introducerades i WMF 5,0 som har till gång till medlemmar i `System.Reflection.RuntimeType` , till exempel `[int].ImplementedInterfaces` . Den här buggen har åtgärd ATS i WMF 5,1.

### <a name="fixed-some-issues-with-com-objects"></a>Åtgärda problem med COM-objekt

WMF 5,0 introducerade en ny COM-bindning för att anropa metoder på COM-objekt och komma åt egenskaper för COM-objekt. Detta nya binder förbättrade prestanda avsevärt men introducerade vissa buggar som har åtgärd ATS i WMF 5,1.

#### <a name="argument-conversions-were-not-always-performed-correctly"></a>Argument konverteringar utfördes inte alltid korrekt

Se följande exempel:

```powershell
$obj = New-Object -ComObject WScript.Shell
$obj.SendKeys([char]173)
```

**SendKeys** -metoden förväntar sig en sträng, men PowerShell konverterade inte Char-tecken till en sträng, som Uppskjut konverteringen till **IDispatch:: Invoke** , som använder **VariantChangeType** för att utföra konverteringen. I det här exemplet har detta resulterat i att skicka nycklarna "1", "7" och "3" i stället för den förväntade **volymen. inaktivera** nyckel.

#### <a name="enumerable-com-objects-not-always-handled-correctly"></a>Enumerable COM-objekt hanteras inte alltid korrekt

PowerShell räknar normalt upp de flesta enumerable-objekt, men en regression som introducerades i WMF 5,0 förhindrade uppräkningen av COM-objekt som implementerar IEnumerable. Exempel:

```powershell
function Get-COMDictionary
{
    $d = New-Object -ComObject Scripting.Dictionary
    $d.Add('a', 2)
    $d.Add('b', 2)
    return $d
}

$x = Get-COMDictionary
```

I exemplet ovan skrev WMF 5,0 felaktigt **skript. ord listan** till pipelinen i stället för att räkna upp nyckel/värde-par.

### <a name="ordered-was-not-allowed-inside-classes"></a>[ordnat] tilläts inte i klasser

WMF 5,0 introducerade klasser med verifiering av typ strängar som används i klasser. `[ordered]` det ser ut som en typ sträng men är inte en äkta .NET-typ. WMF 5,0 rapporterade felaktigt ett fel i `[ordered]` en klass:

```powershell
class CThing
{
    [object] foo($i)
    {
        [ordered]@{ Thing = $i }
    }
}
```

### <a name="help-on-about-topics-with-multiple-versions-does-not-work"></a>Hjälp om ämnen med flera versioner fungerar inte

Innan WMF 5,1, om du hade flera versioner av en modul installerad och alla delade ett hjälp avsnitt, till exempel about_PSReadline, `help about_PSReadline` skulle returnera flera ämnen utan ett uppenbart sätt att visa den riktiga hjälpen.

WMF 5,1 åtgärdar detta genom att returnera hjälpen för den senaste versionen av ämnet.

`Get-Help` innehåller inget sätt att ange vilken version du vill ha hjälp med. Undvik detta genom att navigera till katalogen moduler och visa hjälpen direkt med ett verktyg som din favorit redigerare.

### <a name="powershellexe-reading-from-stdin-stopped-working"></a>powershell.exe läsning från STDIN slutade fungera

Kunder använder `powershell -command -` sig av inbyggda appar för att köra PowerShell genom att skicka skriptet via STDIN. det här har tyvärr avbrutits av andra ändringar i konsol värden.

Detta är åtgärdat för version 5,1 i uppdaterings uppdateringen för Windows 10.

### <a name="powershellexe-creates-spike-in-cpu-usage-on-startup"></a>powershell.exe skapar insamling i CPU-användning vid start

PowerShell använder en WMI-fråga för att kontrol lera om den har startats via grupprincip för att undvika fördröjning i inloggningen. WMI-frågan tar upp inmatnings tzres.mui.dll i varje process på systemet sedan WMI- **Win32_Process** -klassen försöker hämta lokal tids zons information. Detta resulterar i en stor processor ökning i **Wmiprvse** (WMI-providerns värd). Korrigera är att använda Win32 API-anrop för att hämta samma information i stället för att använda WMI.
