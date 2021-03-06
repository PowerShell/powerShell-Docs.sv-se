---
ms.date: 09/13/2016
ms.topic: reference
title: Fel som inte avbryter körningen
description: Fel som inte avbryter körningen
ms.openlocfilehash: d23642103e005c6d3a6168b317b11f40001b6bbe
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/10/2020
ms.locfileid: "92655735"
---
# <a name="non-terminating-errors"></a>Fel som inte avbryter körningen

I det här avsnittet beskrivs den metod som används för att rapportera icke-avslutande fel. Den beskriver också hur du anropar-metoden från cmdleten.

När ett icke-avslutande fel inträffar ska cmdleten rapportera felet genom att anropa metoden [system. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) . När cmdleten rapporterar ett icke-avslutande fel, kan cmdleten fortsätta att arbeta med det här inobjektet och på ytterligare inkommande pipelines-objekt. Om cmdleten anropar metoden [system. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) , kan cmdleten skriva en felpost som beskriver det villkor som orsakade det icke-avslutande fel meddelandet. Mer information om fel poster finns i [fel poster för Windows PowerShell](./windows-powershell-error-records.md).

-Cmdletar kan anropa [system. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) vid behov från sina metoder för bearbetning av indata. Cmdlets kan dock anropa [system. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) endast från den tråd som anropade metoden [system. Management. Automation. cmdlet. BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing), [system. Management. Automation. cmdlet. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)eller [system. Management. Automation. cmdlet. EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) för bearbetnings metoden för indata. Anropa inte [system. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) från en annan tråd. Kommunicera i stället fel i huvud tråden.

## <a name="see-also"></a>Se även

[System. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError)

[System. Management. Automation. cmdlet. BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing)

[System. Management. Automation. cmdlet. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[System. Management. Automation. cmdlet. EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)

[Windows PowerShell-felposter](./windows-powershell-error-records.md)

[Skriva en Windows PowerShell-cmdlet](./writing-a-windows-powershell-cmdlet.md)
