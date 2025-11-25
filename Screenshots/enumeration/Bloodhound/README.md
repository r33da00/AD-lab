# BloodHound Enumeration

## Overview

This guide covers the usage of BloodHound for Active Directory enumeration. BloodHound is a reconnaissance tool that visualizes Active Directory environments, allowing security professionals to identify attack paths and security misconfigurations.

## Prerequisites

Before beginning, ensure you have the following installed:
- BloodHound
- bloodhound-python (BloodHound.py)

## Important Configuration Note

**Critical:** Before running BloodHound.py, configure your domain controller IP as the nameserver in `/etc/resolv.conf` to prevent connectivity issues:

```bash
# Add to /etc/resolv.conf
nameserver <DC_IP_ADDRESS>
```

## Data Collection

BloodHound requires data to function effectively. We'll use bloodhound-python to collect this information remotely.

### Basic Collection

Use credentials obtained from previous enumeration phases (such as password spraying) to gather initial data:

```bash
bloodhound-python -u <username> -p <password> -dc <dc_hostname> -d <domain_name>
```

**Expected Output:** This command generates several JSON files containing enumeration data:
- `users.json` - User account information
- `groups.json` - Group membership data
- `domains.json` - Domain information
- `computers.json` - Computer object details

These files provide comprehensive Active Directory intelligence without requiring a compromised Windows host.

### Comprehensive Collection

For complete enumeration, use the `-c All` parameter to collect all available data:

```bash
bloodhound-python -u <username> -p <password> -dc <dc_hostname> -d <domain_name> -c All
```

**Note:** Remove previous JSON files before running this command to avoid duplicates.

**Tip:** Use a JSON-capable text editor (such as Sublime Text or Visual Studio Code) to review the collected data in a readable format.

## Data Analysis

### Importing Data into BloodHound

1. Launch the BloodHound application
2. Click the **Upload Data** button in the interface
3. Select and upload all generated JSON files

### Exploring the Data

Once imported, BloodHound provides visualization and analysis capabilities for:
- User privileges and permissions
- Group memberships and nesting
- Computer relationships
- Trust relationships
- Attack paths and privilege escalation opportunities
- Kerberos delegation configurations
- Local admin rights mapping

### Key Analysis Features

- **Pre-built Queries:** Use BloodHound's built-in queries to identify common attack paths
- **Custom Queries:** Create custom Cypher queries for specific scenarios
- **Shortest Path Analysis:** Identify the most direct routes to high-value targets
- **Node Information:** Click on any object to view detailed properties and relationships

## Summary

BloodHound provides powerful Active Directory reconnaissance capabilities that can reveal:
- Hidden privilege escalation paths
- Misconfigured permissions
- Over-privileged accounts
- Trust relationship vulnerabilities
- Attack surface analysis

This enumeration phase establishes a foundation for understanding the Active Directory environment and identifying potential security weaknesses.

---

**Next Steps:** Proceed to the next phase of the engagement based on identified vulnerabilities and attack paths.