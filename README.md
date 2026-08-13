# Windows-Least-Privilege-Audit-
# Windows Least Privilege Audit

A Windows CMD-based audit verifying least-privilege access control on a 
workstation — checking whether a standard user account holds excessive 
permissions, and whether default accounts/groups are configured safely.

## Objective
Verify that the Principle of Least Privilege is correctly applied on a 
Windows endpoint — confirming a standard user isn't granted more access 
than necessary.

## Commands Used
| Command | Purpose |
|---|---|
| `whoami` | Identified the current logged-in user |
| `whoami /user` | Retrieved the user's Security Identifier (SID) |
| `whoami /groups` | Listed all group memberships for the current user |
| `whoami /priv` | Listed system privileges assigned to the current user and their state |
| `net localgroup "Administrators"` | Checked membership of the local Administrators group |
| `net localgroup "Remote Desktop Users"` | Checked Remote Desktop access group membership |
| `net localgroup "Remote Management Users"` | Checked WMI/Remote Management access group membership |
| `net user Guest` | Checked the built-in Guest account's status |

## Key Findings
- Standard user account is **not** a member of the local Administrators group — confirms least privilege is being followed for everyday use
- Remote Desktop Users and Remote Management Users groups are both empty — no unnecessary remote access granted
- Most elevated privileges (e.g. system shutdown, docking station removal) are **Disabled** for the standard account
- Guest account is present but **inactive** — reduces attack surface from an unused default account

## What I Learned
- How to verify least-privilege configuration using built-in Windows 
  commands, without third-party tools
- The difference between group membership (`whoami /groups`) and 
  individual privilege assignment (`whoami /priv`)
- Why auditing default/built-in accounts (like Guest) matters as much 
  as auditing custom user accounts
