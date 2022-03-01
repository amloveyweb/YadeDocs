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

### YadeDB

### Playmaker Support

After Playmaker installed in project, we can see the actions in Action Browser. Below is the actions of Yadesheet.

|Action| Description|
|---| ---|
|Get Cell Value |  Get value of cell |
|Get Cell Raw Value | Get raw value of cell |
|Cet Cell Unity Object | Get unity object (texture, material, etc) of the cell |
|Get Cell By Index | Get cell by row and column index |
| Get Cell by Alpha Index | Get cell by alpha based index of row and column |
| Set Cell Raw Value by Alpha Index | set raw value of cell by alpha based index of row and column |
|Set  Cell Raw Value | Set raw value of cell by row and column index |
