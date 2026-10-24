# Exam Notes

## Notes
1. Learn to find references in MS Learn. Challenge yourself in:
    - use Azure CLI, challenge to see how to create resource-group.
    - use ARM template, challenge to see how to create resource-group and storage account.

## Roles
This is nice to go thru [roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles)

## Timing
You have ONLY 2 hours to complete ~60 questions. With that you can only spend an average of 2 minutes per question, so time it properly and if the question seems simple enough just go thru it.

Return to review can risk more time than expected. To actually return to view all questions after review, click on a button on the top left to go back to view all questions. Unlike AWS, once you go to a review question you need to click on the button on the top left to go back to view all questions, else you need to keep clicking NEXT.

### Types of Agents
1. **Azure Site Recovery Agent** - Azure Site Recovery Provider, for disaster recovery
2. **Microsoft Azure Recovery Services Agent** - MARS, requires a MABS to write to.
3. **Azure Diagnostic Agent** - MDA (see Data Collection Rule)
4. **Azure Monitor Agent** - AMA
5. **Azure Log Analytics Agent** - MMA (Legacy)
6. **Network Watcher Agent** - MMA, used to monitor network packets
7. **Network Dependency Agent** - MMA, used to monitor network dependencies

## Azure Files
1. Still one that can use AD for authentication. Identity-based.

## Roles
1. **Contributor** can add/delete but cannot manage users
2. **User Access Administrator** - can manage users and roles.

## Monitor
1. Any Azure Monitor/Dashboard can only have max up to 30days, regardless of logs analytics storage.

## KeyVault
1. Can be backup, but can only RESTORE to:

  - same subscription
  - same geography