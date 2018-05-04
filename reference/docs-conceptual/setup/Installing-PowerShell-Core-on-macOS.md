# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="f78ba-101">Installera PowerShell Core på macOS</span><span class="sxs-lookup"><span data-stu-id="f78ba-101">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="f78ba-102">PowerShell Core stöder macOS 10.12 och högre.</span><span class="sxs-lookup"><span data-stu-id="f78ba-102">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="f78ba-103">Alla paket är tillgängliga på vår GitHub [släpper][] sidan.</span><span class="sxs-lookup"><span data-stu-id="f78ba-103">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="f78ba-104">När paketet har installerats kör `pwsh` från en terminal.</span><span class="sxs-lookup"><span data-stu-id="f78ba-104">Once the package is installed, run `pwsh` from a terminal.</span></span>

### <a name="installation-via-homebrew-on-macos-1012"></a><span data-ttu-id="f78ba-105">Installation via Homebrew på macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="f78ba-105">Installation via Homebrew on macOS 10.12</span></span>

<span data-ttu-id="f78ba-106">[Homebrew] [ brew] är prioriterade package manager för macOS.</span><span class="sxs-lookup"><span data-stu-id="f78ba-106">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="f78ba-107">Om den `brew` kommando inte hittas, måste du installera följande Homebrew [instruktionerna][brew].</span><span class="sxs-lookup"><span data-stu-id="f78ba-107">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="f78ba-108">När du har installerat Homebrew, är det enkelt att installera PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f78ba-108">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="f78ba-109">Installera först [Homebrew Cask][cask], så kan du installera flera paket:</span><span class="sxs-lookup"><span data-stu-id="f78ba-109">First, install [Homebrew-Cask][cask], so you can install more packages:</span></span>

```sh
brew tap caskroom/cask
```

<span data-ttu-id="f78ba-110">Du kan nu installera PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f78ba-110">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="f78ba-111">Kontrollera slutligen att din installera fungerar:</span><span class="sxs-lookup"><span data-stu-id="f78ba-111">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="f78ba-112">När nya versioner av PowerShell släpps uppdatera Homebrews formler och uppgradera PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f78ba-112">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="f78ba-113">Kommandona ovan kan anropas från en värd med PowerShell (pwsh), men sedan PowerShell-gränssnittet måste avslutas och startas om för att slutföra uppgraderingen.</span><span class="sxs-lookup"><span data-stu-id="f78ba-113">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="f78ba-114">och uppdatera värdena som visas i $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="f78ba-114">and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/

### <a name="installation-via-direct-download"></a><span data-ttu-id="f78ba-115">Installationen via direkt hämtning</span><span class="sxs-lookup"><span data-stu-id="f78ba-115">Installation via Direct Download</span></span>

<span data-ttu-id="f78ba-116">Hämta PKG `powershell-6.0.2-osx.10.12-x64.pkg` från den [släpper][] sidan på din dator macOS.</span><span class="sxs-lookup"><span data-stu-id="f78ba-116">Download the PKG package `powershell-6.0.2-osx.10.12-x64.pkg` from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="f78ba-117">Du kan dubbelklicka på filen och följ anvisningarna eller installera det från terminalen:</span><span class="sxs-lookup"><span data-stu-id="f78ba-117">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="f78ba-118">Binär Arkiv</span><span class="sxs-lookup"><span data-stu-id="f78ba-118">Binary Archives</span></span>

<span data-ttu-id="f78ba-119">PowerShell binär `tar.gz` Arkiv som har angetts för macOS- och Linux-plattformar för att aktivera avancerade distribueringsscenarier.</span><span class="sxs-lookup"><span data-stu-id="f78ba-119">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="f78ba-120">Installera binär Arkiv på macOS</span><span class="sxs-lookup"><span data-stu-id="f78ba-120">Installing binary archives on macOS</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.0.2

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.0.2

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.2/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.0.2/pwsh /usr/local/bin/pwsh
```

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="f78ba-121">Avinstallera PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="f78ba-121">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="f78ba-122">Om du har installerat PowerShell med Homebrew är avinstallationen enkel:</span><span class="sxs-lookup"><span data-stu-id="f78ba-122">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="f78ba-123">Om du har installerat PowerShell via direkt hämtning måste PowerShell tas bort manuellt:</span><span class="sxs-lookup"><span data-stu-id="f78ba-123">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="f78ba-124">Om du vill ta bort de ytterligare PowerShell-sökvägarna finns på [sökvägar][] avsnittet i det här dokumentet och ta bort den önskade sökvägar med `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="f78ba-124">To remove the additional PowerShell paths, please see the [paths][] section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="f78ba-125">Detta är inte nödvändigt om du har installerat med Homebrew.</span><span class="sxs-lookup"><span data-stu-id="f78ba-125">This is not necessary if you installed with Homebrew.</span></span>

[sökvägar]:#paths
[paths]:#paths

## <a name="paths"></a><span data-ttu-id="f78ba-127">Sökvägar</span><span class="sxs-lookup"><span data-stu-id="f78ba-127">Paths</span></span>

* <span data-ttu-id="f78ba-128">`$PSHOME` Är `/opt/microsoft/powershell/6.0.0/`</span><span class="sxs-lookup"><span data-stu-id="f78ba-128">`$PSHOME` is `/opt/microsoft/powershell/6.0.0/`</span></span>
* <span data-ttu-id="f78ba-129">Användarprofiler som ska läsas från `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="f78ba-129">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="f78ba-130">Standardprofiler kommer att läsas från `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="f78ba-130">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="f78ba-131">Moduler som användare kommer att läsas från `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="f78ba-131">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="f78ba-132">Delade moduler kommer att läsas från `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="f78ba-132">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="f78ba-133">Standardmoduler ska läsas från `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="f78ba-133">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="f78ba-134">PSReadline historik kommer att läggas till `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="f78ba-134">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="f78ba-135">Profilerna ta hänsyn till konfiguration av PowerShells per värd.</span><span class="sxs-lookup"><span data-stu-id="f78ba-135">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="f78ba-136">Så värd-specifika standardprofiler finns på `Microsoft.PowerShell_profile.ps1` på samma platser.</span><span class="sxs-lookup"><span data-stu-id="f78ba-136">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="f78ba-137">PowerShell respekterar den [XDG Base Directory specifikationen] [ xdg-bds] på macOS.</span><span class="sxs-lookup"><span data-stu-id="f78ba-137">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="f78ba-138">Eftersom macOS är en härledning av BSD prefixet `/usr/local` används i stället för `/opt`.</span><span class="sxs-lookup"><span data-stu-id="f78ba-138">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="f78ba-139">Därför `$PSHOME` är `/usr/local/microsoft/powershell/6.0.0/`, och symlink är placerad på `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="f78ba-139">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.0/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

[släpper]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html