### Runtime API

#### IndexHelper

**Public Static Methods**

| Method | Description |
| ------ | ---- |
| IntToAlphaIndex | Convert int to alhpa based index. For example, 0 to A, 1 to B |
| AlphaToIntIndex | Convert alpha based index to int index. For example, A to 0, B to 1 |
| ToAlphaBasedCellIndex | Get alpha based cell index. For example, (0, 0) => A1, (1, 3) => D2 |
|AlphaBasedToCellIndex|Convert alpha based index to cell index. For example, A1 => (0, 0)|

#### YadeSheetData

**Public Properties**

|Name| Description|
|---|---|
|FormulaEngine|Formula engine inside  sheet|

**Public Fields**

|Name| Description|
|---|---|
| data | Data of rows |
| columnHeaders | Data of column headers|

**Public Methods**

|Name| Description|
|---|---|
| GetColumnCount |  Get columns count of sheet |
| GetRowCount  | Get rows count of the sheet |
| GetCell | Get cell at specific position |

**Extension Methods**


|Name| Description|
|---|---|
| AsList<T> | Parse data to a List<T> |
| AsDictionary<T> | Parse data as Dictionary<T> |

### YadeDatabase

**Public Properties**

|Name| Description|
|---|---|
|Sheets|Sheets in the database |

**Public Methods**

|Name| Description|
|---|---|
| Query(sheetName, alphaIndex) | Query sheet to get a cell by alpha index |
| Query(sheetName, row, column) | Query sheet to get a cell by row and column index |
| Query(sheetName, predicate)| Query sheet to get a collection of typed data |
| Query(sheetNames, predicate) | Query sheets to get a collection of typed data |
| MapQuery(sheetName, predicate) | Query sheet to get a dictionary with the first column of sheet as Keys of the dictionary. Rows with null or empty value of first column will be ignored. |
| QueryByKey(sheetName, key) | Get a typed class row of sheet by key. NOTE: The first column of a row is the key |

### YadeDB

**Public Fields**

|Name| Description|
|---|---|
|DefaultDB|Deafult databse in Resources folder. Value is "YadeDB" |

**Public static methods**

|Name| Description|
|---|---|
| GetDatabase(database) | Get database by name  |
| Q(sheetName, alphaIndex, database) | Query sheet to get a cell by alpha index |
| Q(sheetName, row, column, database) | Query sheet to get a cell by row and column index |
| Q(sheetName, predicate, database) | Query sheet to get a collection of typed data |
| MapQ(sheetName, predicate, database) | Query sheet to get a dictionary with the first column of sheet as Keys of the dictionary. Rows with null value of first column will be ignored.|
| QByKey(sheetName, key, database) | Get a typed class row of sheet by key. NOTE: The first column of a row is the key|

### Playmaker Support

After Playmaker installed in project, we can see the actions in Action Browser. Below is the actions of Yadesheet.

|Action| Description|
|---| ---|
|Get Cell Value |  Get value of cell |
|Get Cell Raw Value | Get raw value of cell |
|Cet Cell Unity Object | Get unity object (texture, material, etc) of the cell |
|Get Cell By Index | Get cell by row and column index |
|Get Cell by Alpha Index | Get cell by alpha based index of row and column |
|Set Cell Raw Value by Alpha Index | set raw value of cell by alpha based index of row and column |
|Set  Cell Raw Value | Set raw value of cell by row and column index |
|Yade DB Query Cell By Alpha Index | Query cell by alpha index using YadeDB |
|Yade DB Query Cell By Index | Query cell by index using YadeDB |
|Yade DB Set Cell Raw Value By Index| Set cell raw value by index using YadeDB|
|Yade DB Set Cell Raw Value By Alpha Index|Set cell raw value by alpha index using YadeDB|

### FlowCanvas Support

Download the FlowCanvas support Unity Package [HERE](https://www.amlovey.com/yadeDocs/Extensions/FlowCanvasIntegration.unitypackage)

|Action| Description|
|---| ---|
|GetSheetCellByAlphaIndex| Get cell by alpha based index |
|GetSheetCellByIndex |Get cell by index|
|SetCellRawValueByIndex| Set raw value of cell by row and column index |
|SetCellRawValueByAlphaIndex|Set raw value of cell by row and column index|
|YadeDatabaseGetSheetCellByAlphaIndex|Get a cell from sheet by alpha index using Yade database|
|YadeDatabaseGetSheetCellByIndex|Get a cell from sheet by index using Yade database|
|GetCellValue|Get value of a cell|
|GetCellRawValue|Get raw value of a cell|
|GetCellUnityObject|Get unity object value of a cell|
