---
external help file: Microsoft.PowerShell.Commands.Management.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Management
ms.date: 01/29/2021
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.management/clear-recyclebin?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Clear-RecycleBin
ms.openlocfilehash: e7ce0f2bcd1ece0bb737aea1297641c37337f3e5
ms.sourcegitcommit: 81558c2adb9d109946a027e5b96e4d24b3b13747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/30/2021
ms.locfileid: "99098691"
---
# Clear-RecycleBin

## SAMMANFATTNING
Rensar innehållet i en pappers korg.

## SYNTAX

### Alla

```
Clear-RecycleBin [[-DriveLetter] <String[]>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## BESKRIVNING

`Clear-RecycleBin`Cmdleten tar bort innehållet i en dators pappers korg. Den här åtgärden påminner om att använda Windows **tomt Pappers korgen**.

Den här cmdleten lades till i PowerShell 7.

## EXEMPEL

### 1: Rensa alla pappers korgar

I det här exemplet rensas alla lokala datorer i pappers korgen.

```powershell
Clear-RecycleBin
```

```Output
Confirm
Are you sure you want to perform this action?
Performing the operation "Clear-RecycleBin" on target "All of the contents of the Recycle Bin".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
```

`Clear-RecycleBin` uppmanas användaren att bekräfta att alla pappers korgar tas bort från den lokala datorn.

### 2: Rensa en angiven pappers korg

I det här exemplet rensas pappers korgen för en angiven enhets beteckning.

```powershell
Clear-RecycleBin -DriveLetter C
```

`Clear-RecycleBin` använder parametern **DriveLetter** för att ange pappers korgen på **C** -volymen. Användaren uppmanas att bekräfta att kommandot ska köras.

### 3: Rensa alla pappers korgar utan bekräftelse

I det här exemplet visas ingen bekräftelse för att ta bort den lokala datorns pappers korg.

```powershell
Clear-RecycleBin -Force
```

`Clear-RecycleBin` använder **Force** -parametern och uppmanas inte användaren att bekräfta att alla pappers korgar tas bort från den lokala datorn.

Ett alternativ är att ersätta `-Force` med `-Confirm:$false` .

## PARAMETRAR

### -DriveLetter

Anger pappers korgen för att rensa en enskild enhets beteckning eller en matris med enhets beteckningar.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Force

Anger att användaren inte behöver bekräfta att en pappers korgen ska rensas. Parametern **Force** åsidosätter också parametrarna **whatIf** och **Confirm** .

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm

Uppmanas att bekräfta användaren innan du kör cmdleten. Användaren uppmanas att bekräfta även om parametern **Confirm** inte har angetts.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf

Visar vad som händer om `Clear-RecycleBin` körs. Cmdleten körs inte.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

Denna cmdlet har stöd för parametrarna -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction och -WarningVariable. Mer information finns i [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INDATA

## UTDATA

### Inget

## ANTECKNINGAR

Den här cmdleten är endast tillgänglig på Windows-plattformar.

## RELATERADE LÄNKAR
