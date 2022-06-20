# YadeDatabase

A database class that manage yadesheets as datatables.

### Public Properties

|Name| Description|
|---|---|
|Sheets|Sheets in the database |
|BinarySerializerEnabled| Turn binary serialization on or off |

### Public Methods

|Name| Description|
|---|---|
| Query(sheetName, alphaIndex) | Query sheet to get a cell by alpha index |
| Query(sheetName, row, column) | Query sheet to get a cell by row and column index |
| Query\<T\>(sheetName, predicate)| Query sheet to get a collection of typed data |
| Query\<T\>(sheetNames, predicate) | Query sheets to get a collection of typed data |
| MapQuery\<T\>(sheetName, predicate) | Query sheet to get a dictionary with the first column of sheet as Keys of the dictionary. Rows with null or empty value of first column will be ignored. |
| QueryByKey\<T\>(sheetName, key) | Get a typed class row of sheet by key. **NOTE: The first column of a row is the key** |
| GetSheetByName(sheetName) | Get yade sheet instance by its name |
| SetRawValue(sheetName, alphaIndex, rawText) | Set raw value of a cell in sheet. **NOTE: ASSET formula does not support in build** |
| SetRawValue(sheetName, row, column, rawText)| Set raw value of a cell in sheet. **NOTE: ASSET formula does not support in build** |
| Serialize | Serialize data to byte array |
| Deserialize | Deserialize byte array to data |

### Code Samples

```csharp
// Define sample data class
public class Data
{
    [DataField(0)] public string A;
    [DataField(1)] public string B;

    // ASSETS() function will mapping to array of Unity Objects,
    // We can use C# array or list to deserialize it.
    [DataField(2)] public Texture2D[] Textures;
}

var sheetName = "TestSheet";

// Query cell by alpha index in a sheet
database.Query(sheetName, "A1");
database.Query(sheetName, 0, 0);

// Query sheet by first column as Key. It will
database.QueryByKey<Data>(sheetName, "KeyOfDictionary");

// Query sheet as a collection with or without conditions
database.Query<Data>(sheetName);
database.Query<Data>(sheetName, item => item.A == "Hello");

// Query sheets as a collection with or without conditions
var sheetNames = new string[] { "TestSheet", "TestSheet1" };
database.Query<Data>(sheetNames);
database.Query<Data>(sheetNames, item => item.A == "Hello");

// Query sheet as dictionary with first column as Keys with
// or without conditions
database.MapQuery<Data>(sheetName);
database.MapQuery<Data>(sheetName, kvp => kvp.Value.B == "World");

// Set raw value of a cell
database.SetRawValue(sheetName, "A1", "Hello");
database.SetRawValue(sheetName, 0, 2, "=SUM(A1:B1)");

// Serialize and Deserialize
database.BinarySerializerEnabled = true;

var bytes = database.Serialize();
database.Deserialize(bytes);
```