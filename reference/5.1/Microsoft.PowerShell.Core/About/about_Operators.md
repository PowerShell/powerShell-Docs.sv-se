---
description: Beskriver de operatorer som stöds av PowerShell.
keywords: powershell,cmdlet
Locale: en-US
ms.date: 11/09/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_operators?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Operators
ms.openlocfilehash: b783d2cb76fe8a0a66ec77b67ef915f3b78def04
ms.sourcegitcommit: 768816a5c05cc2d07ffd84bed95b0499f4b49f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/11/2020
ms.locfileid: "94483014"
---
# <a name="about-operators"></a>Om operatörer

## <a name="short-description"></a>Kort beskrivning
Beskriver de operatorer som stöds av PowerShell.

## <a name="long-description"></a>Lång beskrivning

En operator är ett språk element som du kan använda i ett kommando eller uttryck.
PowerShell stöder flera typer av operatorer som hjälper dig att hantera värden.

### <a name="arithmetic-operators"></a>Aritmetiska operatorer

Använd aritmetiska operatorer ( `+` , `-` ,, `*` `/` , `%` ) för att beräkna värden i ett kommando eller uttryck. Med dessa operatörer kan du lägga till, subtrahera, multiplicera eller dividera värden och beräkna resten (Modulus) för en divisions åtgärd.

Operatorn addition sammanfogar element. Operatorn multiplikation returnerar det angivna antalet kopior av varje element. Du kan använda aritmetiska operatorer på vilken .net-typ som helst som implementerar dem, till exempel: `Int` , `String` ,, `DateTime` `Hashtable` , och matriser.

Bitvisa operatorer (,,,, `-band` `-bor` `-bxor` `-bnot` `-shl` `-shr` ) ändrar bit mönstren i värden.

Mer information finns i [about_Arithmetic_Operators](about_Arithmetic_Operators.md).

### <a name="assignment-operators"></a>Tilldelnings operatörer

Använd tilldelnings operatörer ( `=` ,,,, `+=` `-=` `*=` `/=` `%=` ) för att tilldela, ändra eller lägga till värden för variabler. Du kan kombinera aritmetiska operatorer med tilldelning för att tilldela resultatet av den aritmetiska åtgärden till en variabel.

Mer information finns i [about_Assignment_Operators](about_Assignment_Operators.md).

### <a name="comparison-operators"></a>Jämförelseoperatorer

Använd jämförelse operatorer ( `-eq` ,,,, `-ne` `-gt` `-lt` `-le` `-ge` ) för att jämföra värden och test villkor. Du kan till exempel jämföra två sträng värden för att avgöra om de är lika.

Jämförelse operatorerna innehåller också operatorer som söker efter eller ersätter mönster i text. `-match` `-notmatch` Operatorerna (,, `-replace` ) använder reguljära uttryck och ( `-like` , `-notlike` ) använder jokertecken `*` .

Jämförelse operatorer för inne slutning avgör om ett testvärde visas i en referens uppsättning ( `-in` ,, `-notin` `-contains` , `-notcontains` ).

Skriv jämförelse operatorer ( `-is` , `-isnot` ) för att avgöra om ett objekt är av en specifik typ.

Mer information finns i [about_Comparison_Operators](about_Comparison_Operators.md).

### <a name="logical-operators"></a>Logiska operatorer

Använd logiska operatorer (,,, `-and` `-or` `-xor` `-not` , `!` ) för att ansluta villkorliga uttryck till ett enda komplext villkor. Du kan till exempel använda en logisk `-and` operator för att skapa ett objekt filter med två olika villkor.

Mer information finns i [about_Logical_Operators](about_logical_operators.md).

### <a name="redirection-operators"></a>Operatorer för omdirigering

Använd omdirigerings operatorer (,,, `>` `>>` `2>` `2>>` och `2>&1` ) för att skicka utdata från ett kommando eller uttryck till en textfil. Operatorerna för omdirigering fungerar som `Out-File` cmdlet (utan parametrar), men de låter dig också omdirigera fel utdata till angivna filer. Du kan också använda `Tee-Object` cmdleten för att dirigera om utdata.

Mer information finns i [about_Redirection](about_Redirection.md)

### <a name="split-and-join-operators"></a>Dela och koppla operatörer

`-split` `-join` Operatorerna och delar upp och kombinerar del strängar. `-split`Operatorn delar en sträng i del strängar. `-join`Operatorn sammanfogar flera strängar till en enda sträng.

Mer information finns i [about_Split](about_Split.md) och [about_Join](about_Join.md).

### <a name="type-operators"></a>Typ operatörer

Använd typ operatorer ( `-is` , `-isnot` , `-as` ) för att söka efter eller ändra .NET Framework typ för ett objekt.

Mer information finns i [about_Type_Operators](about_Type_Operators.md).

### <a name="unary-operators"></a>Unära operatorer

Använd unära operatorer för att öka eller minska variabler eller objekt egenskaper och ange heltal till positiva eller negativa tal. Om du till exempel vill öka variabeln `$a` från `9` till `10` skriver du `$a++` .

### <a name="special-operators"></a>Särskilda operatörer

Särskilda operatörer har specifika användnings fall som inte passar in i någon annan operator grupp. Med särskilda operatorer kan du till exempel köra kommandon, ändra värdens datatyp eller hämta element från en matris.

#### <a name="grouping-operator--"></a>Grupp operator `( )`

Precis som på andra språk, kan det `(...)` vara så att operator prioriteten åsidosätts i uttryck. Exempelvis: `(1 + 2) / 3`

I PowerShell finns det dock ytterligare beteenden.

- `(...)` gör att du kan låta utdata från ett _kommando_ delta i ett uttryck. Exempel:

  ```powershell
  PS> (Get-Item *.txt).Count -gt 10
  True
  ```

- När det används som det första segmentet i en pipeline, kan ett kommando eller uttryck i parentes orsaka _uppräkning_ av uttryck resultatet. Om parentesen radbryter ett _kommando_ körs det för att slutföras med alla utdata _som samlats in i minnet_ innan resultatet skickas via pipelinen.

> [!NOTE]
> Att omsluta ett kommando inom parenteser gör att den automatiska variabeln `$?` ställs in på `$true` , även när själva kommandot är inställt `$?` på `$false` .
> Till exempel `(Get-Item /Nosuch); $?` ger den oväntade avkastningen **True**. Mer information om `$?` finns i [about_Automatic_Variables](about_Automatic_Variables.md).

#### <a name="subexpression-operator--"></a>Operator för under uttryck `$( )`

Returnerar resultatet av en eller flera instruktioner. Returnerar en skalär för ett enda resultat. Returnerar en matris för flera resultat. Använd det här när du vill använda ett uttryck i ett annat uttryck. Till exempel för att bädda in resultatet av kommandot i ett sträng uttryck.

```powershell
PS> "Today is $(Get-Date)"
Today is 12/02/2019 13:15:20

PS> "Folder list: $((dir c:\ -dir).Name -join ', ')"
Folder list: Program Files, Program Files (x86), Users, Windows
```

#### <a name="array-subexpression-operator--"></a>Array-underexpress operator `@( )`

Returnerar resultatet av en eller flera uttryck som en matris. Om det bara finns ett objekt har matrisen bara en medlem.

```powershell
@(Get-CimInstance win32_logicalDisk)
```

#### <a name="hash-table-literal-syntax-"></a>Litteral syntax för hash-tabell `@{}`

I likhet med matrisens under uttryck används den här syntaxen för att deklarera en hash-tabell.
Mer information finns i [about_Hash_Tables](about_Hash_Tables.md).

#### <a name="call-operator-"></a>Anrops operator `&`

Kör ett kommando, ett skript eller ett skript block. Anrops operatorn, som även kallas "anrops operatorn", gör att du kan köra kommandon som lagras i variabler och som representeras av strängar eller skript block. Anrops operatorn körs i ett underordnat omfång. Mer information om omfattningar finns [about_Scopes](about_Scopes.md).

Det här exemplet lagrar ett kommando i en sträng och kör det med hjälp av anrops operatorn.

```
PS> $c = "get-executionpolicy"
PS> $c
get-executionpolicy
PS> & $c
AllSigned
```

Anrops operatorn tolkar inte strängar. Det innebär att du inte kan använda kommando parametrar i en sträng när du använder anrops operatorn.

```
PS> $c = "Get-Service -Name Spooler"
PS> $c
Get-Service -Name Spooler
PS> & $c
& : The term 'Get-Service -Name Spooler' is not recognized as the name of a
cmdlet, function, script file, or operable program. Check the spelling of
the name, or if a path was included, verify that the path is correct and
try again.
At line:1 char:2
+ & $c
+  ~~
    + CategoryInfo          : ObjectNotFound: (Get-Service -Name Spooler:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```

Cmdleten [Invoke-Expression](xref:Microsoft.PowerShell.Utility.Invoke-Expression) kan köra kod som orsakar tolkning av fel när anrops operatorn används.

```
PS> & "1+1"
& : The term '1+1' is not recognized as the name of a cmdlet, function, script
file, or operable program. Check the spelling of the name, or if a path was
included, verify that the path is correct and try again.
At line:1 char:2
+ & "1+1"
+  ~~~~~
    + CategoryInfo          : ObjectNotFound: (1+1:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
PS> Invoke-Expression "1+1"
2
```

Du kan använda anrops operatorn för att köra skript med sina fil namn. I exemplet nedan visas ett skript fil namn som innehåller blank steg. När du försöker köra skriptet visar PowerShell i stället innehållet i den citerade strängen som innehåller fil namnet. Med anrops operatorn kan du köra innehållet i strängen som innehåller fil namnet.

```
PS C:\Scripts> Get-ChildItem

    Directory: C:\Scripts


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        8/28/2018   1:36 PM             58 script name with spaces.ps1

PS C:\Scripts> ".\script name with spaces.ps1"
.\script name with spaces.ps1
PS C:\Scripts> & ".\script name with spaces.ps1"
Hello World!
```

Mer information om skript block finns [about_Script_Blocks](about_Script_Blocks.md).

#### <a name="cast-operator--"></a>Omvandlings operator `[ ]`

Konverterar eller begränsar objekt till den angivna typen. Om objekten inte kan konverteras genererar PowerShell ett fel.

```powershell
[DateTime]"2/20/88" - [DateTime]"1/20/88"
[Int] (7/2)
[String] 1 + 0
[Int] '1' + 0
```

En omvandling kan också utföras när en variabel tilldelas till att använda [Cast notation](about_Variables.md).

#### <a name="comma-operator-"></a>Komma-operator `,`

Som en binär operator skapar kommatecknet en matris eller lägger till i matrisen som skapas. I uttrycks läge, som en unär operator, skapar kommatecknet en matris med bara en medlem. Placera kommatecknet före medlemmen.

```powershell
$myArray = 1,2,3
$SingleArray = ,1
Write-Output (,1)
```

Eftersom `Write-Object` ett argument förväntas måste du ange uttrycket inom parentes.

#### <a name="dot-sourcing-operator-"></a>Punkt källa-operator `.`

Kör ett skript i det aktuella omfånget så att alla funktioner, alias och variabler som skriptet skapar läggs till i det aktuella omfånget, vilket åsidosätter befintliga. Parametrar som deklareras av skriptet blir variabler. Parametrar för vilka inget värde har angetts blir variabler utan värde. Den automatiska variabeln `$args` bevaras dock.

```powershell
. c:\scripts\sample.ps1 1 2 -Also:3
```

> [!NOTE]
> Operatorn punkt källa följs av ett blank steg. Använd utrymmet för att skilja pricken från den punkt ( `.` ) symbol som representerar den aktuella katalogen.
>
> I följande exempel körs Sample.ps1-skriptet i den aktuella katalogen i det aktuella omfånget.
>
> ```powershell
> . .\sample.ps1
> ```

#### <a name="format-operator--f"></a>Format operator `-f`

Formaterar strängar med hjälp av metoden format för sträng objekt. Ange format strängen på vänster sida av operatorn och de objekt som ska formateras på höger sida av operatorn.

```powershell
"{0} {1,-10} {2:N}" -f 1,"hello",[math]::pi
```

```output
1 hello      3.14
```

Om du behöver behålla klammerparenteserna ( `{}` ) i den formaterade strängen kan du kringgå dem genom att dubblera klammerparenteserna.

```powershell
"{0} vs. {{0}}" -f 'foo'
```

```Output
foo vs. {0}
```

Mer information finns i metoden [String. format](/dotnet/api/system.string.format) och [sammansatt formatering](/dotnet/standard/base-types/composite-formatting).

#### <a name="index-operator--"></a>Index operator `[ ]`

Väljer objekt från indexerade samlingar, till exempel matriser och hash-tabeller. Mat ris index är noll-baserade, så det första objektet indexeras som `[0]` . För matriser (endast) kan du också använda negativa index för att hämta de sista värdena. Hash-tabeller indexeras efter nyckel värde.

```
PS> $a = 1, 2, 3
PS> $a[0]
1
PS> $a[-1]
3
```

```powershell
(Get-HotFix | Sort-Object installedOn)[-1]
```

```powershell
$h = @{key="value"; name="PowerShell"; version="2.0"}
$h["name"]
```

```output
PowerShell
```

```powershell
$x = [xml]"<doc><intro>Once upon a time...</intro></doc>"
$x["doc"]
```

```output
intro
-----
Once upon a time...
```

#### <a name="pipeline-operator-"></a>Pipeline-operator `|`

Skickar ("pipes") utdata från kommandot som föregår det till kommandot som följer. När utdata innehåller fler än ett objekt (en "samling") skickar pipeline-operatorn objektet en i taget.

```powershell
Get-Process | Get-Member
Get-Service | Where-Object {$_.StartType -eq 'Automatic'}
```

#### <a name="range-operator-"></a>Intervall operator `..`

Representerar sekventiella heltal i en heltals mat ris, med en övre och nedre gränser.

```powershell
1..10
foreach ($a in 1..$max) {Write-Host $a}
```

Du kan också skapa intervall i omvänd ordning.

```powershell
10..1
5..-5 | ForEach-Object {Write-Output $_}
```

#### <a name="member-access-operator-"></a>Ansvarig för medlems åtkomst `.`

Ansluter till egenskaper och metoder för ett objekt. Medlems namnet kan vara ett uttryck.

```powershell
$myProcess.peakWorkingSet
(Get-Process PowerShell).kill()
'OS', 'Platform' | Foreach-Object { $PSVersionTable. $_ }
```

#### <a name="static-member-operator-"></a>Statisk medlems operator `::`

Anropar statiska egenskaper och metoder för en .NET Framework-klass. Om du vill hitta statiska egenskaper och metoder för ett objekt använder du cmdletens statiska parameter `Get-Member` .  Medlems namnet kan vara ett uttryck.

```powershell
[datetime]::Now
'MinValue', 'MaxValue' | Foreach-Object { [int]:: $_ }
```

## <a name="see-also"></a>Se även

[about_Arithmetic_Operators](about_Arithmetic_Operators.md)

[about_Assignment_Operators](about_Assignment_Operators.md)

[about_Comparison_Operators](about_Comparison_Operators.md)

[about_Logical_Operators](about_logical_operators.md)

[about_Operator_Precedence](about_operator_precedence.md)

[about_Type_Operators](about_Type_Operators.md)

[about_Split](about_Split.md)

[about_Join](about_Join.md)

[about_Redirection](about_Redirection.md)
