---
title: WS-Management-fjärrkommunikation (WSMan) i PowerShell Core
description: Fjärr kommunikation i PowerShell Core med WSMan
ms.date: 08/06/2018
ms.openlocfilehash: fdc4159279db28b8ee60bc0853e19512a1f9ec14
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/10/2020
ms.locfileid: "92501311"
---
# <a name="ws-management-wsman-remoting-in-powershell-core"></a>WS-Management-fjärrkommunikation (WSMan) i PowerShell Core

## <a name="instructions-to-create-a-remoting-endpoint"></a>Instruktioner för att skapa en fjärran sluten slut punkt

PowerShell Core-paketet för Windows innehåller ett WinRM-plugin-program ( `pwrshplugin.dll` ) och ett installations skript ( `Install-PowerShellRemoting.ps1` ) i `$PSHome` . De här filerna gör att PowerShell kan acceptera inkommande PowerShell fjärr anslutningar när dess slut punkt anges.

### <a name="motivation"></a>Motivation

En installation av PowerShell kan upprätta PowerShell-sessioner till fjärrdatorer med hjälp av `New-PSSession` och `Enter-PSSession` . För att det ska kunna ta emot inkommande PowerShell-fjärranslutningar måste användaren skapa en WinRM Remoting-slutpunkt. Det här är ett explicit scenario där användaren kör Install-PowerShellRemoting.ps1 för att skapa WinRM-slutpunkten. Installations skriptet är en kortsiktig lösning tills vi lägger till ytterligare funktioner till `Enable-PSRemoting` för att utföra samma åtgärd. Mer information hittar du i problem [#1193](https://github.com/PowerShell/PowerShell/issues/1193).

### <a name="script-actions"></a>Skript åtgärder

Skriptet

1. Skapar en katalog för plugin-programmet i `$env:windir\System32\PowerShell`
1. Kopierar pwrshplugin.dll till den platsen
1. Genererar en konfigurations fil
1. Registrerar plugin-programmet med WinRM

### <a name="registration"></a>Registrering

Skriptet måste köras i en PowerShell-session på administratörs nivå och köras i två lägen.

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a>Körs av den instans av PowerShell som den ska registreras

```powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a>Utföras av en annan instans av PowerShell på uppdrag av den instans som den ska registreras

```powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>"
```

Exempel:

```powershell
Set-Location -Path 'C:\Program Files\PowerShell\6.0.0\'
.\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0\"
```

> [!NOTE]
> Registrerings skriptet för fjärr kommunikation startar om WinRM. Alla befintliga PSRP-sessioner avslutas omedelbart efter att skriptet har körts. Om kör under en fjärrsession avslutar skriptet anslutningen.

## <a name="how-to-connect-to-the-new-endpoint"></a>Så här ansluter du till den nya slut punkten

Skapa en PowerShell-session för den nya PowerShell-slutpunkten genom att ange `-ConfigurationName "some endpoint name"` . Om du vill ansluta till PowerShell-instansen från exemplet ovan använder du antingen:

```powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0"
```

Observera att `New-PSSession` och `Enter-PSSession` anrop som inte anges `-ConfigurationName` kommer att riktas mot standard-PowerShell-slutpunkten `microsoft.powershell` .
