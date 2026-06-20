1. What are event logs?

2. Event Viewer:
Event logs are crucial for troubleshooting any computer incident and help understand the situation and how to remediate the incident. To get this picture well, you must first understand the format in which the information will be presented. Windows offers a standardized means of relaying this system information.
These elements are:
System Logs: Records events associated with the Operating System segments. They may include information about hardware changes, device drivers, system changes, and other activities related to the device.
Security Logs: Records events connected to logon and logoff activities on a device. The system's audit policy specifies the events. The logs are an excellent source for analysts to investigate attempted or successful unauthorized activity.
Application Logs :Records events related to applications installed on a system. The main pieces of information include application errors, events, and warnings.
Directory Service Events: Active Directory changes and activities are recorded in these logs, mainly on domain controllers.
File Replication Service Events: Records events associated with Windows Servers during the sharing of Group Policies and logon scripts to domain controllers, from where they may be accessed by the users through the client servers.
DNS Event Logs: DNS servers use these logs to record domain events and to map out
Custom Logs: Events are logged by applications that require custom data storage. This allows applications to control the log size or attach other parameters, such as ACLs, for security purposes.

There are three main ways of accessing these event logs within a Windows system:
Event Viewer (GUI-based application)
Wevtutil.exe (command-line tool)
Get-WinEvent (PowerShell cmdlet)


3. wevtutil.exe:
Per Microsoft, the wevtutil.exe tool "enables you to retrieve information about event logs and publishers. You can also use this command to install and uninstall event manifests, to run queries, and to export, archive, and clear logs."


