# Blob_Operations

Check who downloaded or uploaded a blob on the Azure Storage Account Container using this KQL query:

```
StorageBlobLogs
| join kind=inner (
    AzureActivity
    | where TenantId == "YOUR TENANT ID"
) on TenantId
| where TimeGenerated >= ago(1d)
| where OperationName == "PutBlob" or OperationName == "GetBlob"
| where parse_json(Properties).caller contains "@"
| project TimeGenerated,ObjectKey, OperationName, StatusText, CallerIpAddress, ServiceType, Caller

```

Out example: 

https://github.com/DavidArayaSanabria/Blob_Operation/blob/53e28ecf44e750d73a4c6c2745ab55c0688b86d6/images/example.png
