
# SQL Server and SMTP Connectivity Checklist

## Overview

This document covers basic connectivity checks for enterprise applications that depend on Microsoft SQL Server or SMTP services.

The examples are general and should be adapted to the approved environment.

## 1. SQL Server Connectivity

When an application cannot connect to its database, check:

- SQL Server service status
- Database server availability
- Correct SQL Server instance
- DNS resolution
- Network connectivity
- Firewall rules
- Database authentication and permissions
- Application error logs

### Basic Network Test

From an authorized Windows system, PowerShell can be used to check TCP connectivity:

```powershell
Test-NetConnection -ComputerName sql.example.com -Port 1433
```

Port 1433 is commonly used for SQL Server, but the actual port may differ.

A successful TCP test confirms that the port is reachable. It does not confirm that database authentication or queries will work.

## 2. SMTP Connectivity

When application emails or notifications are not working, check:

- SMTP server availability
- Correct server address and port
- DNS resolution
- Network connectivity
- Authentication settings
- TLS requirements
- Sender permissions
- Application logs

### Basic SMTP Network Test

```powershell
Test-NetConnection -ComputerName smtp.example.com -Port 587
```

Port 587 is commonly used for authenticated SMTP submission.

A successful TCP connection does not confirm that authentication, TLS negotiation or email delivery will succeed.

## 3. Application Service Checks

If the application is not communicating with its dependencies:

1. Check whether the application service is running.
2. Review Windows Event Viewer.
3. Review application-specific logs.
4. Verify the required network connections.
5. Check service account permissions.
6. Confirm that dependent services are available.

## 4. Common Issues

| Issue | Initial Check |
|---|---|
| SQL connection timeout | Network, firewall and SQL service |
| Database login failure | Authentication and database permissions |
| SMTP connection failure | Server address, port and network |
| Email authentication error | SMTP credentials and authentication settings |
| Email not delivered | Application logs and mail server response |
| Application service fails | Dependencies and event logs |

## 5. Troubleshooting Process

1. Identify the reported issue.
2. Confirm which service is affected.
3. Review relevant error messages.
4. Test connectivity from an authorized system.
5. Check application and server logs.
6. Escalate changes requiring additional permissions.
7. Document the findings and resolution.

## Security Notes

- Never publish database passwords or SMTP credentials.
- Do not upload real application configuration files.
- Use example hostnames in public documentation.
- Follow approved access and change procedures.

## Note

All hostnames in this document are illustrative. These checks are not evidence of testing a specific production environment.
