---
ms.date: 09/13/2016
ms.topic: reference
title: Lägga till parametrar som bearbetar pipelineindata
description: Lägga till parametrar som bearbetar pipelineindata
ms.openlocfilehash: b150d5be93207d9c010a6d2d4de901b4526f1d79
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/10/2020
ms.locfileid: "92668362"
---
# <a name="adding-parameters-that-process-pipeline-input"></a>Lägga till parametrar som bearbetar pipelineindata

En källa för indata för en cmdlet är ett objekt i pipelinen som härstammar från en överordnad cmdlet. I det här avsnittet beskrivs hur du lägger till en parameter i Get-Proc-cmdleten (beskrivs i [skapa din första cmdlet](./creating-a-cmdlet-without-parameters.md)) så att cmdleten kan bearbeta pipeline-objekt.

Denna Get-Proc-cmdlet använder en `Name` parameter som accepterar indata från ett pipeline-objekt, hämtar process information från den lokala datorn baserat på de angivna namnen och visar sedan information om processerna på kommando raden.

## <a name="defining-the-cmdlet-class"></a>Definiera cmdlet-klassen

Det första steget i att skapa en cmdlet namnger alltid cmdleten och deklarerar den .NET-klass som implementerar cmdleten. Den här cmdleten hämtar process information, så verbet som väljs här är "Get". (Nästan alla sorters cmdlets som kan hämta information kan bearbeta kommando rads indata.) Mer information om godkända cmdlet-verb finns i [cmdlet-verb](./approved-verbs-for-windows-powershell-commands.md).

Följande är definitionen för denna Get-Proc-cmdlet. Information om den här definitionen anges i [skapa din första cmdlet](./creating-a-cmdlet-without-parameters.md).

```csharp
[Cmdlet(VerbsCommon.Get, "proc")]
public class GetProcCommand : Cmdlet
```

```vb
<Cmdlet(VerbsCommon.Get, "Proc")> _
Public Class GetProcCommand
    Inherits Cmdlet
```

## <a name="defining-input-from-the-pipeline"></a>Definiera ininformation från pipelinen

I det här avsnittet beskrivs hur du definierar ininformation från pipelinen för en cmdlet. Den här Get-Proc cmdleten definierar en egenskap som representerar `Name` parametern enligt beskrivningen i [lägga till parametrar som bearbetar kommando rads indatatyper](./adding-parameters-that-process-command-line-input.md).
(Se avsnittet för allmän information om att deklarera parametrar.)

Men när en cmdlet måste bearbeta pipeline-inmatade, måste den ha sina parametrar som är kopplade till indatavärden av Windows PowerShell-körningsmiljön. Om du vill göra detta måste du lägga till `ValueFromPipeline` nyckelordet eller lägga till `ValueFromPipelineByProperty` nyckelordet i deklarationen för attributet [system. Management. Automation. Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) . Ange `ValueFromPipeline` nyckelordet om cmdleten får åtkomst till det kompletta indatamängden. Ange `ValueFromPipelineByProperty` om cmdlet: en får åtkomst till en egenskap för objektet.

Här är parameter deklarationen för `Name` parametern för den här Get-Proc cmdleten som godkänner pipeline-inflöden.

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample03/GetProcessSample03.cs" range="35-44":::

```vb
<Parameter(Position:=0, ValueFromPipeline:=True, _
ValueFromPipelineByPropertyName:=True), ValidateNotNullOrEmpty()> _
Public Property Name() As String()
    Get
        Return processNames
    End Get

    Set(ByVal value As String())
        processNames = value
    End Set

End Property
```

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesgetproc03#GetProc03VBNameParameter](Msh_samplesgetproc03#GetProc03VBNameParameter)]  -->

I den föregående deklarationen anges `ValueFromPipeline` nyckelordet till `true` så att Windows PowerShell-körningsmiljön binder parametern till det inkommande objektet om objektet är av samma typ som parametern, eller om den kan tvingas till samma typ. `ValueFromPipelineByPropertyName`Nyckelordet är också inställt på `true` så att Windows PowerShell-körningsmiljön kontrollerar det inkommande objektet för en `Name` egenskap. Om det inkommande objektet har en sådan egenskap, kommer körningen att binda `Name` parametern till `Name` egenskapen för det inkommande objektet.

> [!NOTE]
> Inställningen av `ValueFromPipeline` nyckelordet attribut för en parameter har företräde framför inställningen för `ValueFromPipelineByPropertyName` nyckelordet.

## <a name="overriding-an-input-processing-method"></a>Åsidosätta en metod för bearbetning av indata

Om cmdleten ska hantera pipeline-indata måste den åsidosätta lämpliga metoder för bearbetning av indata. De grundläggande metoderna för indata-bearbetning införs när [du skapar din första cmdlet](./creating-a-cmdlet-without-parameters.md).

Den här Get-Proc cmdleten åsidosätter metoden [system. Management. Automation. cmdlet. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) för att hantera `Name` parameter indata från användaren eller ett skript. Med den här metoden hämtas processerna för varje begärt process namn eller alla processer om inget namn anges. Observera att i [system. Management. Automation. cmdlet. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), anropet till [WriteObject (system. Object, system. Boolean)](/dotnet/api/system.management.automation.cmdlet.writeobject#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) är utmatnings mekanismen för att skicka utgående objekt till pipelinen. Den andra parametern för det här anropet, `enumerateCollection` , är inställd på `true` att meddela Windows PowerShell-körningsmiljön att räkna upp matrisen med process objekt och skriva en process i taget till kommando raden.

```csharp
protected override void ProcessRecord()
{
  // If no process names are passed to the cmdlet, get all processes.
  if (processNames == null)
  {
      // Write the processes to the pipeline making them available
      // to the next cmdlet. The second argument of this call tells
      // PowerShell to enumerate the array, and send one process at a
      // time to the pipeline.
      WriteObject(Process.GetProcesses(), true);
  }
  else
  {
    // If process names are passed to the cmdlet, get and write
    // the associated processes.
    foreach (string name in processNames)
    {
      WriteObject(Process.GetProcessesByName(name), true);
    } // End foreach (string name...).
  }
}
```

```vb
Protected Overrides Sub ProcessRecord()
    Dim processes As Process()

    '/ If no process names are passed to the cmdlet, get all processes.
    If processNames Is Nothing Then
        processes = Process.GetProcesses()
    Else

        '/ If process names are specified, write the processes to the
        '/ pipeline to display them or make them available to the next cmdlet.
        For Each name As String In processNames
            '/ The second parameter of this call tells PowerShell to enumerate the
            '/ array, and send one process at a time to the pipeline.
            WriteObject(Process.GetProcessesByName(name), True)
        Next
    End If

End Sub 'ProcessRecord
```

## <a name="code-sample"></a>Kod exempel

Den fullständiga exempel koden för C# finns i [GetProcessSample03-exempel](./getprocesssample03-sample.md).

## <a name="defining-object-types-and-formatting"></a>Definiera objekt typer och formatering

Windows PowerShell skickar information mellan cmdlets med .net-objekt. Därför kan en cmdlet behöva definiera en egen typ, eller så kan cmdleten behöva utöka en befintlig typ som tillhandahålls av en annan cmdlet. Mer information om hur du definierar nya typer eller utökar befintliga typer finns i [utöka objekt typer och formatering](/previous-versions//ms714665(v=vs.85)).

## <a name="building-the-cmdlet"></a>Skapa cmdleten

När du har implementerat en cmdlet måste den vara registrerad med Windows PowerShell via en Windows PowerShell-snapin-modul. Mer information om att registrera cmdlets finns i [så här registrerar du cmdlets, providers och värd program](/previous-versions//ms714644(v=vs.85)).

## <a name="testing-the-cmdlet"></a>Testa cmdleten

När din cmdlet har registrerats med Windows PowerShell kan du testa den genom att köra den på kommando raden. Testa till exempel koden för exempel-cmdlet: en. Mer information om hur du använder cmdlets från kommando raden finns i [komma igång med Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell).

- I Windows PowerShell-prompten anger du följande kommandon för att hämta process namnen via pipelinen.

  ```powershell
  PS> type ProcessNames | get-proc
  ```

  Följande utdata visas.

  ```
  Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)    Id  ProcessName
  -------  ------  -----   ----- -----   ------    --  -----------
      809      21  40856    4448    147    9.50  2288  iexplore
      737      21  26036   16348    144   22.03  3860  iexplore
       39       2   1024     388     30    0.08  3396  notepad
     3927      62  71836   26984    467  195.19  1848  OUTLOOK
  ```

- Ange följande rader för att hämta de process objekt som har en `Name` egenskap från processerna som kallas "iexplore". I det här exemplet används `Get-Process` cmdlet (från Windows PowerShell) som ett uppströms kommando för att hämta processerna "iexplore".

  ```powershell
  PS> get-process iexplore | get-proc
  ```

  Följande utdata visas.

  ```
  Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)    Id  ProcessName
  -------  ------  -----   ----- -----   ------    --  -----------
      801      21  40720    6544    142    9.52  2288  iexplore
      726      21  25872   16652    138   22.09  3860  iexplore
      801      21  40720    6544    142    9.52  2288  iexplore
      726      21  25872   16652    138   22.09  3860  iexplore
  ```

## <a name="see-also"></a>Se även

[Lägga till parametrar som bearbetar kommando rads indatatyper](./adding-parameters-that-process-command-line-input.md)

[Skapa din första cmdlet](./creating-a-cmdlet-without-parameters.md)

[Utöka objekt typer och formatering](/previous-versions//ms714665(v=vs.85))

[Registrera cmdlets, providers och värd program](/previous-versions//ms714644(v=vs.85))

[Windows PowerShell-referens](../windows-powershell-reference.md)

[Cmdlet-exempel](./cmdlet-samples.md)
