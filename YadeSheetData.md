# YadeSheetData

### Public Properties

|Name| Description|
|---|---|
|FormulaEngine|Formula engine inside  sheet|
|BinarySerializerEnabled| Turn binary serialization on or off |

### Public Fields

|Name| Description|
|---|---|
| data | Data of rows |
| columnHeaders | Data of column headers|

### Public Methods

|Name| Description|
|---|---|
| GetColumnCount |  Get columns count of sheet |
| GetRowCount  | Get rows count of the sheet |
| GetCell | Get cell at specific position |

### Extension Methods


|Name| Description|
|---|---|
| AsList\<T\> | Deserialize data to a List<T> |
| AsDictionary\<T\> | Deserialize data as Dictionary<T> |
| SetRawValue | Set raw value of cell |
| Serialize | Serialize data to byte array |
| Deserialize | Deserialize byte array to data |
| CopyTo | Copy sheet data to another YadeSheet |

### Code Samples

``` csharp
// ------Basic Operation-------------------//

// Get row count of yadesheet
int rowCount = yadesheet.GetRowCount();

// Get column count of yadesheet
int columCount = yadesheet.GetColumnCount();

// Get a cell of yade sheet
var cell = yadesheet.GetCell(0, 0)
var cellByAlpha = yadesheet.GetCell("B1");

// Set raw value of a cell
yadesheet.SetRawValue(0, 0, "Hello");
yadesheet.SetRawValue("C1", "=SUM(A1:B1)")


// ------Deserialize to C# Objects----------//

// Define sample data class
public class Data
{
    [DataField(0)] public int A;
    [DataField(1)] public string B;

    // ASSETS() function will mapping to array of Unity Objects,
    // We can use C# array or list to deserialize it.
    [DataField(2)] public Texture2D[] Textures;
}

// Deserialize to list
var list = yadesheet.AsList<Data>();

// Deserialize to dictionary with column A as key
var dict = yadesheet.AsDictionary<int, Data>(data => data.A);


// ------Binary Serialization--------------//

// Below is samples for binary serialization
// We have to set turn on the binary serialization
// before we modify sheet data
yadesheet.BinarySerializerEnabled = true;

// Then Serialize to sheet
var bytes = yadesheet.Serialize();

// And deserilize later from bytes
yadesheet.Deserialize(bytes);

// -------Data Copy---------------------//
YadeSheetData other = ScriptableObject.CreateInstance<YadeSheetData>();
yadesheet.CopyTo(other);
```