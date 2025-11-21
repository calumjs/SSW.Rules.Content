---
seoDescription: Verify your server meets minimum requirements before upgrading software, ensuring compatibility with newer versions and preventing potential issues.
type: rule
archivedreason:
title: Do you verify that your server meets the minimum requirements?
guid: 8ffc9f7c-63fe-4e43-ba3c-bd88f892eb9b
uri: do-you-verify-that-your-server-meets-the-minimum-requirements
created: 2015-08-12T15:12:25.0000000Z
authors: []
related: []
redirects: []
---

Whenever you upgrade infrastructure software, double-check that your servers, clients, SQL tiers, and build agents meet the requirements for the version you are deploying. This is especially important for Team Foundation Server (TFS) and its successor, Azure DevOps Server, because each release tightens the list of supported operating systems, databases, and hardware profiles.

Team Foundation Server 2015 leaves extended support on October 14, 2025, so stop validating against old release-candidate requirements and plan your upgrade path to Azure DevOps Server 2022.2 or the newly rebranded “Azure DevOps Server” (no year) now ([Azure DevOps lifecycle update](https://devblogs.microsoft.com/devops/upcoming-support-lifecycle-milestones-for-older-on-premises-products/), [Microsoft lifecycle](https://learn.microsoft.com/en-us/lifecycle/products/visual-studio-team-foundation-server-2015), [branding announcement](https://devblogs.microsoft.com/devops/announcing-the-new-azure-devops-server-rc-release/)). That upgrade path is fully supported directly from TFS 2015, so there is no benefit in holding onto prerelease artifacts that no longer exist.

<!--endintro-->

**What to validate today**

* Confirm your platform against the current [Azure DevOps Server requirements](https://learn.microsoft.com/en-us/azure/devops/server/requirements?view=azure-devops-2022). Azure DevOps Server 2022.x supports Windows Server 2022 or Windows Server 2019 for the application tier, Windows 11 Version 21H2 or Windows 10 1809+ for clients, and the latest “Azure DevOps Server” build adds Windows Server 2025 support, so align your plans with that matrix instead of obsolete RC guidance.
* Use the same [requirements doc](https://learn.microsoft.com/en-us/azure/devops/server/requirements?view=azure-devops-2022) to size hardware realistically: Microsoft recommends a single-server deployment with an octa-core CPU, 16 GB RAM, and SSD storage (plus two dual-core CPUs with 8 GB RAM for Elastic/Code Search), and calls for dedicated 16 GB SSD-backed application and data tiers once you grow beyond roughly 500 users.
* Verify SQL Server support (Azure SQL Database, Azure SQL Managed Instance, SQL Server 2022, or SQL Server 2019) and keep build/test agents off the application tier so automated workloads never starve the core service. Use the [requirements matrix](https://learn.microsoft.com/en-us/azure/devops/server/requirements?view=azure-devops-2022) to match supported versions before every upgrade.

**Practical workflow**

* Before every upgrade, grab the current requirements article, compare it with your inventory (OS versions, SQL build, hardware specs, domain functional level), and create a punch list of gaps against Microsoft’s supported matrix ([requirements](https://learn.microsoft.com/en-us/azure/devops/server/requirements?view=azure-devops-2022)).
* Run the upgrade in a pre-production environment using the latest Azure DevOps Server installer, resolve blockers (unsupported Windows releases, insufficient RAM, deprecated SQL versions), then cut over production once the dry run is stable ([Azure DevOps lifecycle update](https://devblogs.microsoft.com/devops/upcoming-support-lifecycle-milestones-for-older-on-premises-products/)).
* After go-live, monitor the Azure DevOps Blog’s lifecycle posts for new deadlines so your environment never drifts back onto unsupported platforms ([Azure DevOps Blog](https://devblogs.microsoft.com/devops/)).
