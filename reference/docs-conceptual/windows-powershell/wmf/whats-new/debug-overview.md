---
ms.date: 06/12/2017
keywords: WMF, powershell, inställning
title: Förbättringar i felsökning av PowerShell-skript
description: WMF 5,0 lägger till nya fel söknings funktioner i Windows-PoowerShell.
ms.openlocfilehash: 5703343e1b85024931638e8b04a09f7208ea123c
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/27/2020
ms.locfileid: "92646738"
---
# <a name="improvements-in-powershell-script-debugging"></a>Förbättringar i felsökning av PowerShell-skript

PowerShell 5,0 innehåller flera förbättringar som förbättrar fel söknings upplevelsen.

## <a name="break-all"></a>Bryt alla

Med PowerShell-konsolen och PowerShell ISE kan du nu dela upp det i fel söknings programmet för skript körning. Detta fungerar både i lokala och fjärranslutna sessioner.

Tryck på <kbd>CTRL</kbd> + <kbd>Break</kbd>i-konsolen.

Tryck på <kbd>CTRL</kbd> + <kbd>B</kbd>i ISE eller Använd kommandot **Debug-> Bryt alla** Meny kommandon.

## <a name="remote-debugging-and-remote-file-editing-in-powershell-ise"></a>Fjärrfelsökning och fjärrstyrd fil redigering i PowerShell ISE

Nu kan du öppna och redigera filer i en fjärrsession med PowerShell ISE genom att köra kommandot PSEdit.
Du kan till exempel öppna en fil för redigering från kommando raden i en fjärrsession enligt följande:

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

Dessutom kan du nu redigera och spara ändringar i en fjärrfil som öppnas automatiskt i PowerShell ISE när du trycker på en Bryt punkt. Nu kan du Felsöka en skript fil som körs på en fjärrdator, redigera filen för att åtgärda ett fel och sedan köra det ändrade skriptet igen.

## <a name="advanced-script-debugging"></a>Avancerad skript fel sökning

Det finns nya, avancerade fel söknings funktioner som gör att du kan ansluta till en lokal dator process som har läst in PowerShell och felsöka godtyckliga körnings utrymmen i den processen.

### <a name="runspace-debugging"></a>Körnings utrymme-felsökning

Nya cmdletar har lagts till som gör att du kan lista aktuella körnings utrymmen i en process och koppla PowerShell-konsolen eller PowerShell ISE-felsökaren till den körnings utrymme för skript fel sökning:

- Get-Runspace
- Debug-Runspace
- Enable-RunspaceDebug
- Disable-RunspaceDebug
- Get-RunspaceDebug

### <a name="attach-to-process-hosting-powershell"></a>Ansluta till process hosting PowerShell

Nu kan du ansluta till en dator process som har PowerShell inläst. Du gör detta genom att ange en interaktiv session med värd processen. Mer information finns i:

- [Retur-PSHostProcess](/powershell/module/Microsoft.PowerShell.Core/Enter-PSHostProcess)
- [Avsluta-PSHostProcess](/powershell/module/Microsoft.PowerShell.Core/Exit-PSHostProcess)
