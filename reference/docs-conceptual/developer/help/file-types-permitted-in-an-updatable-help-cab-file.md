---
ms.date: 03/22/2012
ms.topic: reference
title: Filtyper som tillåts i en CAB-fil för uppdateringsbar hjälp
description: Filtyper som tillåts i en CAB-fil för uppdateringsbar hjälp
ms.openlocfilehash: bb69b8b89a9a3a5c8c00059ec404a4d41a5db9a5
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/10/2020
ms.locfileid: "92654733"
---
# <a name="file-types-permitted-in-an-updatable-help-cab-file"></a>Filtyper som tillåts i en CAB-fil för uppdateringsbar hjälp

Okomprimerat innehåll i CAB-filen är begränsat till 1 GB som standard. För att kringgå den här gränsen måste användarna använda **Force** -parametern för cmdletarna [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) och [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) .

För att garantera säkerheten för hjälpfiler som hämtas från Internet, kan en uppdaterings bar hjälp CAB-fil endast innehålla de filtyper som anges nedan. Cmdlet: en [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) verifierar alla filer mot hjälp avsnittets scheman. Om `Update-Help` cmdleten påträffar en fil som är ogiltig eller inte är en tillåten typ, installerar den inte den ogiltiga filen och slutar att installera filer från CAB-filen på användarens dator.

- XML-baserade hjälp avsnitt för cmdletar.
- XML-baserade hjälp avsnitt för skript och funktioner.
- XML-baserade hjälp avsnitt för PowerShell-leverantörer.
- Textbaserade hjälp avsnitt, till exempel om ämnen.

[Uppdaterings hjälpen](/powershell/module/Microsoft.PowerShell.Core/Update-Help) verifierar innehållet i CAB-filen när den packar upp CAB-filen. Om `Update-Help` hittar icke-kompatibla filtyper i en uppdaterings bar CAB-fil, genererar den ett avslutande fel och stoppar åtgärden. Det installerar inte några hjälpfiler från CAB-filen, även de som är kompatibla med filtyper.
