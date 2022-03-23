# YadeDB

YadeDatabase Utilites. The YadeDatabase asset should be binplaced under **Resources** folder. otherwise, this utilites will not working for the database.

### Public Fields

|Name| Description|
|---|---|
|DefaultDB|Deafult databse in Resources folder. Value is "YadeDB" |

### Public static methods

|Name| Description|
|---|---|
| GetDatabase(database) | Get database by name  |
| Q(sheetName, alphaIndex, database) | Query sheet to get a cell by alpha index |
| Q(sheetName, row, column, database) | Query sheet to get a cell by row and column index |
| Q\<T\>(sheetName, predicate, database) | Query sheet to get a collection of typed data |
| MapQ\<T\>(sheetName, predicate, database) | Query sheet to get a dictionary with the first column of sheet as Keys of the dictionary. Rows with null value of first column will be ignored.|
| QByKey\<T\>(sheetName, key, database) | Get a typed class row of sheet by key. NOTE: The first column of a row is the key|
| SetRawValue(sheetName, alphaIndex, rawText) | Set raw value of a cell in sheet. **NOTE: ASSET formula does not support in build** |
| SetRawValue(sheetName, row, column, rawText)| Set raw value of a cell in sheet. **NOTE: ASSET formula does not support in build** |
| Serialize | Serialize data to byte array |
| Deserialize | Deserialize byte array to data |
| SetBinarySerializerEnabled | Turn binary serialization on or off |

### Code Samples

```csharp
// "YadeDB" is the default database name in yade.
// It's same value as YadeDB.DefaultDB const string
var dbName = "YadeDB";
var db = YadeDB.GetDatabase(dbName);

// ------------------------------------------------//
// ---BELOW SAMPLES WILL USE DEFAULT DATABASE -----//
// ------------------------------------------------//
var sheetName = "TestSheet";

// Define sample data class
public class Data
{
    [DataField(0)] public string A;
    [DataField(1)] public string B;
}

// Query a cell
var cell = YadeDB.Q(sheetName, "A1");
var cellByIndex = YadeDB.Q(sheetname, 0, 0);

// Query a cell by key, the key is the first column value
var data = YadeDB.Q<Data>(sheetName, "Hello");

// Query sheet as a collection with or without conditions
YadeDB.Q<Data>(sheetName);
YadeDB.Q<Data>(sheetName, item => item.A == "Hello");

// Query sheet as dictionary with first column as Keys with
// or without conditions
YadeDB.MapQ<Data>(sheetName)
YadeDB.MapQ<Data>(sheetName, kvp => kvp.Value.B == "World");

// Set raw value of a cell
YadeDB.SetRawValue(sheetName, "A1", "Hello");
YadeDB.SetRawValue(sheetName, 0, 2, "=SUM(A1:B1)");

// Serialize and Deserialize
YadeDB.SetBinarySerializerEnabled(true);
var bytes = YadeDB.Serialize();
YadeDB.Deserialize(bytes);
```