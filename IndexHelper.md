# IndexHelper

### Public Static Methods

| Method | Description |
| ------ | ---- |
| IntToAlphaIndex | Convert int to alhpa based index. For example, 0 to A, 1 to B |
| AlphaToIntIndex | Convert alpha based index to int index. For example, A to 0, B to 1 |
| ToAlphaBasedCellIndex | Get alpha based cell index. For example, (0, 0) => A1, (1, 3) => D2 |
|AlphaBasedToCellIndex|Convert alpha based index to cell index. For example, A1 => (0, 0)|

### Code Samples

```csharp
// Convert int to alhpa based index. Below sample will return `A`
IndexHelper.IntToAlphaIndex(0);

// Convert alpha based index to int index. Below sample will return 0
IndexHelper.AlphaToIntIndex("A");

// Get alpha based cell index. Below sample will return A1
IndexHelper.ToAlphaBasedCellIndex(0, 0);

// Convert alpha based index to cell index. Below sample will
// return cell index class instance, that both of row index 
// and column index are zero
IndexHelper.AlphaBasedToCellIndex("A1");
```
