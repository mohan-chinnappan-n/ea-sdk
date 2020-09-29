# SOQL execution

## Query
- Success
 ```sql
SELECT Id,Email,Name2 FROM User
```

- Failed
```sql
SELECT Id,Email,Name2 FROM User
```

## Payload

- Success
```json

{
  "messages": [
    {
      "actions": [
        {
          "id": "73;a",
          "descriptor": "serviceComponent://ui.insights.components.wavePage.WavePageAuraController/ACTION$executeSoqlQuery",
          "callingDescriptor": "UNKNOWN",
          "params": {
            "query": "SELECT Id,Email,Name FROM User\n"
          }
        }
      ]
    },
    {
      "actions": [
        {
          "id": "74;a",
          "descriptor": "serviceComponent://ui.insights.components.wavePage.WavePageAuraController/ACTION$postLoglines",
          "callingDescriptor": "UNKNOWN",
          "params": {
            "input": {
              "loglines": [
                {
                  "logLineCode": "iebpf",
                  "fields": {
                    "sessionId": "0c9e8273-df6a-4a7b-bbba-976a17e4b3ad",
                    "timestamp": 1601399984163,
                    "type": "QUERY_TIME",
                    "baseRoute": "dashboard",
                    "subRoute": "0FK3h000000Fel3GAC/view",
                    "tabId": "dashboard-0FK3h000000Fel3GAC",
                    "queryId": 5,
                    "querySequenceId": 12,
                    "querySourceType": "sobject",
                    "result": "SUCCESS",
                    "isCached": false,
                    "duration": 355.9599999571219,
                    "wasBackgrounded": false,
                    "stalledTime": 1.7849999712780118,
                    "transferSize": 3990
                  }
                }
              ]
            }
          }
        }
      ]
    }
  ]
}

```
- Failed
```json

{
  "messages": [
    {
      "actions": [
        {
          "id": "77;a",
          "descriptor": "serviceComponent://ui.insights.components.wavePage.WavePageAuraController/ACTION$executeSoqlQuery",
          "callingDescriptor": "UNKNOWN",
          "params": {
            "query": "SELECT Id,Email,Name2 FROM User\n"
          }
        }
      ]
    },
    {
      "actions": [
        {
          "id": "78;a",
          "descriptor": "serviceComponent://ui.insights.components.wavePage.WavePageAuraController/ACTION$postLoglines",
          "callingDescriptor": "UNKNOWN",
          "params": {
            "input": {
              "loglines": [
                {
                  "logLineCode": "iebpf",
                  "fields": {
                    "sessionId": "0c9e8273-df6a-4a7b-bbba-976a17e4b3ad",
                    "timestamp": 1601400177917,
                    "type": "QUERY_TIME",
                    "baseRoute": "dashboard",
                    "subRoute": "0FK3h000000Fel3GAC/view",
                    "tabId": "dashboard-0FK3h000000Fel3GAC",
                    "queryId": 6,
                    "querySequenceId": 15,
                    "querySourceType": "sobject",
                    "result": "FAILURE",
                    "isCached": false,
                    "errorCode": "130",
                    "duration": 283.4700000239536,
                    "wasBackgrounded": false,
                    "stalledTime": 1.6850000247359276,
                    "transferSize": 4154
                  }
                }
              ]
            }
          }
        }
      ]
    }
  ]
}

````
