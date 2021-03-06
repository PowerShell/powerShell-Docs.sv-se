---
external help file: Microsoft.WSMan.Management.dll-Help.xml
keywords: powershell,cmdlet
Locale: en-US
Module Name: Microsoft.WSMan.Management
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/microsoft.wsman.management/disconnect-wsman?view=powershell-7&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Disconnect-WSMan
ms.openlocfilehash: a754b6530ecd8b3153d82327a246cbb387d53dd5
ms.sourcegitcommit: de63e9481cf8024883060aae61fb02c59c2de662
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/03/2020
ms.locfileid: "93262737"
---
# Disconnect-WSMan

## SAMMANFATTNING
Kopplar från klienten från WinRM-tjänsten på en fjärrdator.

## SYNTAX

```
Disconnect-WSMan [[-ComputerName] <String>] [<CommonParameters>]
```

## BESKRIVNING
Cmdleten **unconnect-WSMan** kopplar från klienten från WinRM-tjänsten på en fjärrdator.
Om du sparade WS-Management-sessionen i en variabel, behålls sessionsobjekt i variabeln, men läget för WS-Management-sessionen stängs.
Du kan använda den här cmdleten i kontexten för WSMan-providern för att koppla bort klienten från WinRM-tjänsten på en fjärrdator.
Du kan också använda denna cmdlet för att koppla från WinRM-tjänsten på fjärrdatorer innan du byter till WSMan-providern.

Mer information om hur du ansluter till WinRM-tjänsten på en fjärrdator finns i Connect-WSMan.

## EXEMPEL

### Exempel 1: ta bort en anslutning till en fjärran sluten dator

```
PS C:\> Disconnect-WSMan -computer server01
PS C:\> cd WSMan:
PS WSMan:\>
PS WSMan:\> dir
WSManConfig: Microsoft.WSMan.Management\WSMan::WSMan
ComputerName                                  Type
------------                                  ----
localhost                                     Container
```

Det här kommandot tar bort anslutningen till fjärrdatorn med namnet Server01.

Denna cmdlet används vanligt vis inom kontexten för WSMan-providern för att koppla från en fjärrdator, i det här fallet Server01-datorn.
Du kan dock också använda **Koppla från-WSMan** för att ta bort anslutningar till fjärrdatorer innan du byter till WSMan-providern.
Dessa anslutningar visas inte i listan dator namn.

## PARAMETRAR

### -ComputerName
Anger den dator som hanterings åtgärden ska köras mot.
Värdet kan vara ett fullständigt kvalificerat domän namn, ett NetBIOS-namn eller en IP-adress.
Använd namnet på den lokala datorn, Använd localhost eller Använd en punkt (.) för att ange den lokala datorn.
Den lokala datorn är standard.
Om fjärrdatorn finns i en annan domän än användaren måste du använda ett fullständigt kvalificerat domän namn.
Du kan skicka ett värde för den här parametern till cmdlet: en.

Det går inte att koppla från den lokala värden.
Det går inte att koppla från standard anslutningen till den lokala datorn.
Men om du skapar en separat anslutning till den lokala datorn, till exempel, med hjälp av dator namnet.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
Denna cmdlet har stöd för parametrarna -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction och -WarningVariable. Mer information finns i [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INDATA

### Inget
Denna cmdlet accepterar inte några indatatyper.

## UTDATA

### Inget
Denna cmdlet genererar inga utdata.

## ANTECKNINGAR

## RELATERADE LÄNKAR

[Anslut-WSMan](Connect-WSMan.md)

[Disable-WSManCredSSP](Disable-WSManCredSSP.md)

[Aktivera – WSManCredSSP](Enable-WSManCredSSP.md)

[Get-WSManCredSSP](Get-WSManCredSSP.md)

[Get-WSManInstance](Get-WSManInstance.md)

[Invoke-WSManAction](Invoke-WSManAction.md)

[New-WSManInstance](New-WSManInstance.md)

[New-WSManSessionOption](New-WSManSessionOption.md)

[Remove-WSManInstance](Remove-WSManInstance.md)

[Set-WSManInstance](Set-WSManInstance.md)

[Set-WSManQuickConfig](Set-WSManQuickConfig.md)

[Test-WSMan](Test-WSMan.md)
