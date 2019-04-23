---
title: Java sample and tutorial for SQL Server 2019 - SQL Server Machine Learning Services
description: Run Java sample code on SQL Server 2019 to learn steps for using the Java language extension with SQL Server data.
ms.prod: sql
ms.technology: machine-learning

ms.date: 04/23/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: ">=sql-server-ver15||=sqlallproducts-allversions"
---

# SQL Server Regex Java Sample

This example demonstrates a Java class that receives two columns (ID and text) from SQL Server, and also takes a regular expression as an input parameter. The class returns two columns back to SQL Server (ID and text).

For a given text in the text column sent to the Java class, the code checks if the given regular expression is fulfilled, and returns that text together with the original ID. 

This particular sample uses a regular expression that checks if a text contains the word "Java" or "java".

## Microsoft Extensibility SDK for Java for Microsoft SQL Server

 In CTP 2.5, we are changing the way you implement Java code that uses the Java language extension to communicate with SQL Server. This will provide a better developer experience when interacting with SQL Server from Java.

You should think about the SDK as a helper interface, that will make it easier to implement Java code running against SQL Server.

> [!NOTE]
> The introduction of the SDK is a big change from previous CTPs. Any previous samples you had working will need to be updated to use the SDK.

For more information, see the [SDK documentation](java-sdk.md).

## Prerequisites

+ SQL Server 2019 Database Engine instance with the extensibility framework and Java programming extension [on Windows](../install/sql-machine-learning-services-windows-install.md) or [on Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup). For more information on system configuration, see [Java language extension in SQL Server 2019](extension-java.md). For more information about coding requirements, see [How to call Java in SQL Server](howto-call-java-from-sql.md).

+ SQL Server Management Studio or Azure Data Studio for running T-SQL.

+ Java SE Development Kit (JDK) 8 or JRE 8 on Windows or Linux.

+ [Microsoft Java Extensibility SDK for Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension) mssql-java-lang-extension.jar.

Command-line compilation using **javac** is sufficient for this tutorial.

## 1 - Create sample data in a SQL Server table

First, create and populate a *testdata* table with **ID** and **text** columns. Connect to SQL Server and run the following script to create a table:

```sql
CREATE DATABASE javatest
GO
USE javatest
GO

-- Create table for test data
DROP TABLE IF exists testdata;
GO

CREATE TABLE testdata(
id int NOT NULL,
"text" nvarchar(100) NOT NULL)
GO

TRUNCATE TABLE testdata
GO

-- Insert data into test table
INSERT INTO testdata(id, "text") VALUES (1, 'This sentence contains java')
INSERT INTO testdata(id, "text") VALUES (2, 'This sentence does not')
INSERT INTO testdata(id, "text") VALUES (3, 'I love Java!')
GO
Select * FROM testdata
```

## 2 - Class RegexSample.java

Start by creating the main class.

In this step, create a class called **RegexSample.java** and copy the following Java code into that file.

This main class is importing the SDK, which means that the jar file downloaded in step1 needs to be discoverable from this class.

> [!NOTE]
> Note that this class imports the Java extension SDK package.
See the article about the [Microsoft Extensibility SDK for Java for Microsoft SQL Server](java-sdk.md) for more details.

```java
package pkg;

import com.microsoft.sqlserver.javalangextension.PrimitiveDataset;
import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionExecutor;
import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.ListIterator;
import java.util.regex.*;

public class RegexSample extends AbstractSqlServerExtensionExecutor {
    private Pattern expr;

    public RegexSample() {
        // Setup the expected extension version, and class to use for input and output dataset
        executorExtensionVersion = SQLSERVER_JAVA_LANG_EXTENSION_V1;
        executorInputDatasetClassName = PrimitiveDataset.class.getName();
        executorOutputDatasetClassName = PrimitiveDataset.class.getName();
    }
    
    public PrimitiveDataset execute(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Validate the input parameters and input column schema
        validateInput(input, params);

        int[] inIds = input.getIntColumn(0);
        String[] inValues = input.getStringColumn(1);
        int rowCount = inValues.length;

        String regexExpr = (String)params.get("regexExpr");
        expr = Pattern.compile(regexExpr);

        System.out.println("regex expression: " + regexExpr);

        // Lists to store the output data
        LinkedList<Integer> outIds = new LinkedList<Integer>();
        LinkedList<String> outValues = new LinkedList<String>();

        // Evaluate each row
        for(int i = 0; i < rowCount; i++) {
            if (check(inValues[i])) {
                outIds.add(inIds[i]);
                outValues.add(inValues[i]);
            }
        }

        int outputRowCount = outValues.size();

        int[] idOutputCol = new int[outputRowCount];
        String[] valueOutputCol = new String[outputRowCount];

        // Convert the list of output columns to arrays
        outValues.toArray(valueOutputCol);

        ListIterator<Integer> it = outIds.listIterator(0);
        int rowId = 0;

        System.out.println("Output data:");
        while (it.hasNext()) {
            idOutputCol[rowId] = it.next().intValue();

            System.out.println("ID: " + idOutputCol[rowId] + " Value: " + valueOutputCol[rowId]);
            rowId++;
        }

        // Construct the output dataset
        PrimitiveDataset output = new PrimitiveDataset();

        output.addColumnMetadata(0, "ID", java.sql.Types.INTEGER, 0, 0);
        output.addColumnMetadata(1, "Text", java.sql.Types.NVARCHAR, 0, 0);

        output.addIntColumn(0, idOutputCol, null);
        output.addStringColumn(1, valueOutputCol);

        return output;
    }

    private void validateInput(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Check for the regex expression input parameter
        if (params.get("regexExpr") == null) {
            throw new IllegalArgumentException("Input parameter 'regexExpr' is not found");
        }

        // The expected input schema should be at least 2 columns, (INTEGER, STRING)
        if (input.getColumnCount() < 2) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }

        // Check that the input column types are expected
        if (input.getColumnType(0) != java.sql.Types.INTEGER &&
                (input.getColumnType(1) != java.sql.Types.VARCHAR && input.getColumnType(1) == java.sql.Types.NVARCHAR )) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }
    }

    private boolean check(String text) {
        Matcher m = expr.matcher(text);

        return m.find();
    }
}
```

## 3 Compile and create .jar file

We recommend that you package your classes and dependencies into .jar files. Most Java IDEs like Eclipse or IntelliJ support generating jar files when you build/compile the project. In this sample, we have named the jar file **regex.jar**.

If you are manually creating a .jar file, you can follow the steps, see [How to create a jar file](extension-java.md#create-jar).

> [!NOTE]
> This sample is using packages, which means that the package "pkg" given at the top of the class makes sure the compiled code is saved in a sub folder called "pkg". This is automatically taken care of if you use an IDE, but if you are manually compiling classes using **javac**, you will need to place the compiled code in the pkg sub folder manually.

## 4 - Create external libraries

By creating an external library, SQL Server will automatically have access to the jar files and you do not need to set any special permissions to the classpath.

In this sample, you will need to create two external libraries. One for the SDK, and one for the Regex Java sample.

1.  Download [Microsoft Extensibility SDK for Java for Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension) mssql-java-lang-extension.jar.

1. Create external library for the sdk

```sql
-- Create external library for the SDK
CREATE EXTERNAL LIBRARY sdk
FROM (CONTENT = '<path>/mssql-java-lang-extension.jar')
WITH (LANGUAGE = 'Java');
GO
```

3. Create external library for the regex sample

```sql
-- Create external library for the regex sample
CREATE EXTERNAL LIBRARY regex
FROM (CONTENT = '<path>/regex.jar')
WITH (LANGUAGE = 'Java');
GO
```

## 5 - Set permissions (Skip if you performed step 4)

This step is not needed if you use external libraries. The recommended way of working is to create an external library from you jar.

If you don't want to use external libraries, you will need to set the necessary permissions. Script execution only succeeds if the process identities have access to your code. You can find more information about setting permissions [here](extension-java.md).

### On Linux

Grant read/execute permissions on the classpath to the **mssql_satellite** user.

### On Windows

Grant 'Read and Execute' permissions to **SQLRUserGroup** and the **All application packages** SID on the folder containing your compiled Java code. 

The entire tree must have permissions, from root parent to the last sub folder. 
 
1. Right-click the folder (for example, 'C:\myJavaCode'), choose **Properties** > **Security**.
2. Click **Edit**.
3. Click **Add**.
4. In **Select Users, Computer, Service Accounts, or Groups**:
   + Click **Object Types** and make sure *Built-in security principles* and *Groups* are selected.
   + Click **Locations** to select the local computer name at the top of the list.
5. Enter **SQLRUserGroup**, check the name, and then click OK to add the group.
6. Enter **ALL APPLICATION PACKAGES**, check the name, and then click OK to add. If the name doesn't resolve, revisit the Locations step. The SID is local to your machine.

Make sure both security identities have 'Read and Execute' permissions on the folder and "pkg" sub folder.

<a name="call-method"></a>

## 2 - Call the Java class

To call the Java code from SQL Server, we will create a stored procedure that calls sp_execute_external_script. In the "script" parameter, we will define which [package].[class] we want to call. In this sample, the class belongs to a package called **pkg** and a class file called **RegexSample.java**.

> [!NOTE]
>We are not defining which method to call. By default, the **execute** method will be called. This means that you need to follow the SDK interface and implement an execute method in your Java class, if you want to be able to call the class from SQL Server.

```sql
/*
This stored procedure takes an input query (input dataset) and a regular expression and returns the rows that fulfilled the given regular expression. This sample uses a regular expression that checks if a text contains the word "Java" or "java" ([Jj]ava) 
*/

CREATE OR ALTER PROCEDURE [dbo].[java_regex] @expr nvarchar(200), @query nvarchar(400)
AS
BEGIN
--Call the Java program by giving the package.className in @script
--The method invoked in the Java code is always the "execute" method
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.RegexSample'
, @input_data_1 = @query
, @params = N'@regexExpr nvarchar(200)'
, @regexExpr = @expr
with result sets ((ID int, text nvarchar(100)));
END
GO

--Now execute the above stored procedure and provide the regular expression and an input query
EXECUTE [dbo].[java_regex] N'[Jj]ava', N'SELECT id, text FROM testdata'
GO
```

### Results

After executing the call, you should get a result set with two of the rows.

![Results from Java sample](../media/java/java-sample-results.png "Sample results")

### If you get an error

+ When you compile your classes, the "pkg" sub folder should contain the compiled code for all three classes.

+ Finally, if you are not using external libraries, check permissions on *each* folder, from root to "pkg" sub folder, to ensure that the security identities running the external process have permission to read and execute your code.

## Next steps

+ [Microsoft Extensibility SDK for Java for Microsoft SQL Server](java-sdk.md)
+ [How to call Java in SQL Server](howto-call-java-from-sql.md)
+ [Java extensions in SQL Server](extension-java.md)
+ [Java and SQL Server data types](java-sql-datatypes.md)
