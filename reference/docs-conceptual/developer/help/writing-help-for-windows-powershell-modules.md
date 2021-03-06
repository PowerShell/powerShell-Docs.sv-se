---
ms.date: 04/10/2020
ms.topic: reference
title: Skriva hjälp för PowerShell-moduler
description: Skriva hjälp för PowerShell-moduler
ms.openlocfilehash: 3bef45c0dd8a7e63bc419bb3e5a7a1783810105b
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/10/2020
ms.locfileid: "92654660"
---
# <a name="writing-help-for-powershell-modules"></a>Skriva hjälp för PowerShell-moduler

PowerShell-moduler kan innehålla hjälp avsnitt om modulen och om modul medlemmar, till exempel cmdlets, providrar, funktioner och skript. `Get-Help`Cmdleten visar hjälp avsnitten för modulen i samma format som den visar hjälp för andra PowerShell-objekt och användare använder standard `Get-Help` kommandon för att hämta hjälp avsnitten.

I det här dokumentet beskrivs formatet och rätt placering av hjälp avsnitt för moduler, och det föreslår rikt linjer för hjälp innehåll i modulen.

## <a name="types-of-module-help"></a>Typer av modul-hjälp

En modul kan innehålla följande typer av hjälp.

- **Cmdlet-hjälp**. Hjälp avsnitten som beskriver cmdlets i en modul är XML-filer som använder kommandot hjälp schema för kommandot

- **Leverantörs hjälp**. Hjälp avsnitten som beskriver leverantörer i en modul är XML-filer som använder providerns hjälp schema.

- **Funktions hjälp**. Hjälp avsnitten som beskriver funktioner i en modul kan vara XML-filer som använder kommandot hjälp schema eller kommentarer baserade hjälp avsnitt i funktionen, skript-eller skript-modulen

- **Skript hjälp**. De hjälp avsnitt som beskriver skript i en modul kan vara XML-filer som använder kommandot hjälp schema eller kommentarer baserade hjälp avsnitt i skript-eller skript-modulen.

- **Konceptuell ("About") hjälp**. Du kan använda ett konceptuellt hjälp avsnitt för att beskriva modulen och dess medlemmar och förklara hur medlemmarna kan användas tillsammans för att utföra uppgifter.
  Konceptuella hjälp ämnen är textfiler med Unicode-kodning (UTF-8). Fil namnet måste använda `about_<name>.help.txt` formatet, till exempel `about_MyModule.help.txt` . Som standard innehåller PowerShell över 100 av dessa begrepp om hjälp avsnitt och de formateras som i följande exempel.

  ```Output
  TOPIC
      about_<subject or module name>

  SHORT DESCRIPTION
      A short, one-line description of the topic contents.

  LONG DESCRIPTION
      A detailed, full description of the subject or purpose of the module.

  EXAMPLES
      Examples of how to use the module or how the subject feature works in practice.

  KEYWORDS
      Terms or titles on which you might expect your users to search for the information in this topic.

  SEE ALSO
      Text-only references for further reading. Hyperlinks cannot work in the PowerShell console.

  ```

Du hittar alla schemafiler i `$PSHOME\Schemas\PSMaml` mappen.

## <a name="placement-of-module-help"></a>Placering av modulens hjälp

`Get-Help`Cmdleten söker efter modulens hjälp ämnes filer i språkspecifika under kataloger i modulens katalog.

Följande katalog struktur diagram visar till exempel platsen för hjälp avsnitten för SampleModule-modulen.

```
<ModulePath>
         \SampleModule
               \<en-US>
                     \about_SampleModule.help.txt
                     \SampleModule.dll-help.xml
                     \SampleNestedModule.dll-help.xml
               \<fr-FR>
                     \about_SampleModule.help.txt
                     \SampleModule.dll-help.xml
                     \SampleNestedModule.dll-help.xml

```

> [!NOTE]
> I exemplet `<ModulePath>` representerar plats hållaren en av Sök vägarna i `PSModulePath` miljö variabeln, till exempel `$HOME\Documents\Modules` , `$PSHOME\Modules` eller en anpassad sökväg som användaren anger.

## <a name="getting-module-help"></a>Hjälp för att hämta modul

När en användare importerar en modul till en session, importeras hjälp avsnitten för modulen till sessionen tillsammans med modulen. Du kan visa hjälp ämnets filer i värdet för nyckeln FileList i modulen manifest, men hjälp ämnen påverkas inte av `Export-ModuleMember` cmdleten.

Du kan tillhandahålla hjälp avsnitt för moduler på olika språk. `Get-Help`Cmdleten visar automatiskt hjälp avsnitt för modulen på det språk som har angetts för den aktuella användaren i objektet nationella inställningar och språk inställningar på kontroll panelen. I Windows Vista och senare versioner av Windows kan du `Get-Help` söka efter hjälp avsnitten i språkspecifika under kataloger i modulens katalog i enlighet med de språk reserv standarder som har upprättats för Windows.

Från och med PowerShell 3,0 körs ett `Get-Help` kommando för en cmdlet eller funktion som aktiverar automatisk import av modulen. `Get-Help`Cmdleten visar omedelbart innehållet i hjälp avsnitten i modulen.

Om modulen inte innehåller hjälp ämnen och det inte finns några hjälp avsnitt för kommandona i modulen på användarens dator, `Get-Help` visar den automatiskt genererade hjälpen. Den automatiskt genererade hjälpen innehåller kommandosyntaxen, parametrarna och indata-och utdatatyperna, men innehåller inte några beskrivningar. Den automatiskt genererade hjälpen innehåller text som instruerar användaren att försöka använda `Update-Help` cmdleten för att hämta hjälp för kommandot från Internet eller en fil resurs. Det rekommenderar också att du  använder `Get-Help` cmdleten online för att hämta online-versionen av hjälp avsnittet.

## <a name="supporting-updatable-help"></a>Stöd för uppdateringsbar hjälp

Användare av PowerShell 3,0 och senare versioner av PowerShell kan ladda ned och installera uppdaterade hjälpfiler för en modul från Internet eller från en lokal fil resurs. `Update-Help` `Save-Help` Cmdletarna och döljer hanterings detaljerna från användaren. Användare kör `Update-Help` cmdleten och använder sedan `Get-Help` cmdleten för att läsa de senaste hjälpfilerna för modulen i PowerShell-Kommandotolken.
Användarna behöver inte starta om Windows eller PowerShell.

Användare bakom brand väggar och sådana utan Internet åtkomst kan också använda uppdaterings bara hjälp.
Administratörer med Internet åtkomst använder `Save-Help` cmdleten för att hämta och installera de senaste hjälpfilerna till en fil resurs. Sedan använder användarna **Sök vägs** parametern för `Update-Help` cmdleten för att hämta de senaste hjälpfilerna från fil resursen.

Module-författare kan inkludera hjälpfiler i modulen och använda uppdaterings bara hjälp för att uppdatera hjälpfilerna eller utelämna hjälpfiler från modulen och använda uppdaterings bara hjälp både för att installera och uppdatera dem.

Mer information om uppdaterings bar hjälp finns i [support uppdaterings bara hjälp](./supporting-updatable-help.md).

## <a name="supporting-online-help"></a>Stöd för onlinehjälp

Användare som inte kan eller inte installerar uppdaterade hjälpfiler på sina datorer förlitar sig ofta på online-versionen av hjälp avsnitten för modulen. Cmdleten **online** för `Get-Help` cmdlet: en öppnar online-versionen av en cmdlet eller ett avancerad funktions hjälp avsnitt för användaren i standard webbläsaren.

`Get-Help`Cmdlet: en använder värdet för **HelpUri** -egenskapen för cmdleten eller funktionen för att hitta online-versionen av hjälp avsnittet.

Från och med PowerShell 3,0 kan du hjälpa användarna att hitta online-versionen av cmdlet-och Function-hjälp avsnitten genom att definiera attributet HelpUri i cmdlet-klassen eller egenskapen **HelpUri** för attributet **CmdletBinding** . Värdet för attributet är värdet för **HelpUri** -egenskapen för cmdleten eller funktionen.

Mer information finns i [support online-hjälpen](./supporting-online-help.md).

## <a name="see-also"></a>Se även

[Skriva en PowerShell-modul](../module/writing-a-windows-powershell-module.md)

[Stöd för uppdateringsbar hjälp](./supporting-updatable-help.md)

[Stöd för onlinehjälp](./supporting-online-help.md)
