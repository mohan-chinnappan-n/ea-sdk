# How to execute run SAQL in Apex

## Topics

- [Execute one query](#q1)
- [Execute 2 queries](#q2)


<a name='q1'></a>
### Create apex code file
```
$ cat ~/.ea/fruits.cls
```

```java
 Wave.ProjectionNode[] projs = new Wave.ProjectionNode[]{
        Wave.QueryBuilder.count().alias('count')
};
    
ConnectApi.LiteralJson result = Wave.QueryBuilder.load('0Fb3h0000005ZoNCAU', '0Fc3h000002yVYPCA2')
    .group(new String[]{'all'})
    .foreach(projs)
    .execute('q');
String response = result.json;
System.debug(result.json);

```

- Note the result will be written to the debug log

### Run it

```
$ sfdx mohanc:tooling:execute  -u mohan.chinnappan.n_ea2@gmail.com  -a ~/.ea/fruits.cls 
apexCode: Wave.ProjectionNode[] projs = new Wave.ProjectionNode[]{
        Wave.QueryBuilder.count().alias('count')
};
    
ConnectApi.LiteralJson result = Wave.QueryBuilder.load('0Fb3h0000005ZoNCAU', '0Fc3h000002yVYPCA2')
    .group(new String[]{'all'})
    .foreach(projs)
    .execute('q');
String response = result.json;
System.debug(result.json);

compiled?: true
executed?: true
{
  line: -1,
  column: -1,
  compiled: true,
  success: true,
  compileProblem: null,
  exceptionStackTrace: null,
  exceptionMessage: null
}

```

<a name='q2'></a>
## Let us execute 2 queries

### Apex code
```   
$ cat ~/.ea/fruits2.cls
Wave.ProjectionNode[] projs = new Wave.ProjectionNode[]{
        Wave.QueryBuilder.count().alias('count')
};
    
ConnectApi.LiteralJson result = Wave.QueryBuilder.load('0Fb3h0000005ZoNCAU', '0Fc3h000002yVYPCA2')
    .group(new String[]{'all'})
    .foreach(projs)
    .execute('q');
String response = result.json;
System.debug(result.json);

 


//==========
Wave.ProjectionNode[] projs2 = new Wave.ProjectionNode[]{
        Wave.QueryBuilder.get('qty').sum().alias('qty_sum')                                  
};
    
    
ConnectApi.LiteralJson result2 = Wave.QueryBuilder.load('0Fb3h0000005ZoNCAU', '0Fc3h000002yVYPCA2')
    .group(new String[]{'name'})
    .foreach(projs2)
    .execute('q');
String response2 = result2.json;
System.debug(result2.json);

// If you excecute both queries, you will get
// Error: System.CalloutException: You have uncommitted work pending. Please commit or rollback before calling out
```

### Run it
```
$ sfdx mohanc:tooling:execute  -u mohan.chinnappan.n_ea2@gmail.com  -a ~/.ea/fruits2.cls 
apexCode: Wave.ProjectionNode[] projs = new Wave.ProjectionNode[]{
        Wave.QueryBuilder.count().alias('count')
};
    
ConnectApi.LiteralJson result = Wave.QueryBuilder.load('0Fb3h0000005ZoNCAU', '0Fc3h000002yVYPCA2')
    .group(new String[]{'all'})
    .foreach(projs)
    .execute('q');
String response = result.json;
System.debug(result.json);


//==========
Wave.ProjectionNode[] projs2 = new Wave.ProjectionNode[]{
        Wave.QueryBuilder.get('qty').sum().alias('qty_sum')                                  
};
    
    
ConnectApi.LiteralJson result2 = Wave.QueryBuilder.load('0Fb3h0000005ZoNCAU', '0Fc3h000002yVYPCA2')
    .group(new String[]{'name'})
    .foreach(projs2)
    .execute('q');
String response2 = result2.json;
System.debug(result2.json);

// If you excecute both queries, you will get
// Error: System.CalloutException: You have uncommitted work pending. Please commit or rollback before calling out

compiled?: true
executed?: false
{
  line: 28,
  column: 1,
  compiled: true,
  success: false,
  compileProblem: null,
  exceptionStackTrace: 'Class.ConnectApi.Wave.executeQuery: line 28, column 1\n' +
    'Class.Wave.QueryNode.execute: line 95, column 1\n' +
    'AnonymousBlock: line 24, column 1\n' +
    'AnonymousBlock: line 24, column 1',
  exceptionMessage: 'System.CalloutException: You have uncommitted work pending. Please commit or rollback before calling out'
}
```

