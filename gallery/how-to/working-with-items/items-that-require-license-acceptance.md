---
ms.date: 06/12/2017
contributor: Farehar
keywords: galleriet powershell psgallery
title: Kräv godkännande av licens
ms.openlocfilehash: 69787cdb12aa47223072551c9b68fc046573f022
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/17/2018
---
# <a name="require-license-acceptance"></a>Kräv godkännande av licens

Kräv godkännande av licens text visas på informationssidan för objektet för moduler som kräver godkännande av licens. Licens för modulen kan visas genom att klicka på länken ”Visa License.txt'.

![Kräv godkännande av licens](../../Images/RequireLicenseAcceptance.png)

Användarna uppmanas att godkänna licensavtalet när du installerar, spara eller uppdatera modulen via PowerShellGet eller när du distribuerar till Azure Automation.

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a>Kräv godkännande av licensen vid distribution till Azure Automation

Om modulen som distribueras på Azure Automation kräver godkännande av licens, portalens användargränssnitt visar en friskrivning som säger ”den här modulen kräver godkännande av licens. Genom att klicka på OK, accepterar licensvillkoren ”.

![Distribuera till Azure Automation kräver godkännande av licens](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a>Mer information

[Kräv godkännande av licens i PowerShellGet](../../concepts/module-license-acceptance.md)
[Azure Automation-webbplats](/azure/automation)