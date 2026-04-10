# Monitoring

## Basic Monitoring
Includes:
- VM availability
- CPU usage percentage (average)
- OS disk usage (total), not data disk
- Network operations (total)
- Disk operations per second (average)

## DCR for Guest OS
To collect metrics and logs from guest OS and client workloads and applications, you need to install Azure Monitor Agent and set up a DCR.

**DCRs** define what data to collect and where to send that data. You can use a DCR to send Azure Monitor metrics data, or performance counters, to Azure Monitor Logs or Azure Monitor Metrics. You can also send event log data to Azure Monitor Logs. 

This can be enabled in Insights or installed manually, just Select the Azure Monitor Agent when you enable VM insights.
![Enable VM Insights](img/enable_vm_insights.png)

## Metrics
- **Azure Monitor Metrics** can store only metrics data
- **Azure Monitor Logs** can store both metrics and event logs.
- Azure Monitor doesn't collect logs by default. You need to install Azure Monitor Agent and set up a DCR to collect logs.
- Azure Monitor stores collected log data in a Log Analytics workspace. 
- Retains the data for 93 days with some exceptions.

## Insights
To gather Guest OS, enable it.
![Insights](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/5-enable-vm-insights)