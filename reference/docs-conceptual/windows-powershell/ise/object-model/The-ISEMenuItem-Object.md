---
ms.date: 12/31/2019
title: ISEMenuItem-objektet
description: Ett ISEMenuItem-objekt är en instans av klassen Microsoft. PowerShell. Host. ISE. ISEMenuItem. Alla meny objekt på menyn **tilläggsprogram** är instanser av klassen ISEMenuItem.
ms.openlocfilehash: 15036e3551687a21dfbe50834a89247c80949656
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/27/2020
ms.locfileid: "92663437"
---
# <a name="the-isemenuitem-object"></a>ISEMenuItem-objektet

Ett **ISEMenuItem** -objekt är en instans av klassen **Microsoft. PowerShell. Host. ISE. ISEMenuItem** .
Alla meny objekt på menyn **tilläggsprogram** är instanser av klassen **Microsoft. PowerShell. Host. ISE. ISEMenuItem** .

## <a name="properties"></a>Egenskaper

### <a name="displayname"></a>DisplayName

Stöds i Windows PowerShell ISE 2,0 och senare.

Den skrivskyddade egenskapen som hämtar meny alternativets visnings namn.

```powershell
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName
```

### <a name="action"></a>Åtgärd

Stöds i Windows PowerShell ISE 2,0 och senare.

Den skrivskyddade egenskapen som hämtar skript blocket. Den anropar åtgärden när du klickar på meny alternativet.

```powershell
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a>Genvägar

Stöds i Windows PowerShell ISE 2,0 och senare.

Den skrivskyddade egenskapen som hämtar kortkommandot för Windows-indatapanelen för meny alternativet.

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a>Inga undermenyer

Stöds i Windows PowerShell ISE 2,0 och senare.

Den skrivskyddade egenskapen som hämtar listan över meny alternativets [undermenyer](The-ISEMenuItemCollection-Object.md) .

```powershell
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a>Skript exempel

Läs igenom följande skript exempel om du vill veta mer om hur du använder menyn tillägg och dess skript bara egenskaper.

```powershell
# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('_Process', {Get-Process}, 'Alt+P')
# Add a nested menu - a parent and a child submenu item.
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('Parent', $null, $null)
$parentAdded.SubMenus.Add('_Dir', {dir}, 'Alt+D')
```

## <a name="see-also"></a>Se även

- [ISEMenuItemCollection-objektet](The-ISEMenuItemCollection-Object.md)
- [Användningsområden för Windows PowerShell ISE-skriptobjektmodellen](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Objekt modells-hierarkin för ISE](The-ISE-Object-Model-Hierarchy.md)
