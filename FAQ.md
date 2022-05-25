# FAQ
<p>
<details>
  <summary> <b>1. Odin Inspector show reference of Yadesheet type field of MonoBehaviour scripts is missing after double click or exiting play mode</b></summary>
  <p>
  Please let your MonoBehaviour script inheirt the `YadeSerializedMonoBehaviour` class, this will fix the issue.
</details>

<p>
<details>
<summary><b>2. Our Google Sheets or Excel have meta data to define type, filed and alias, how to import into Yadesheet with header mapping?</b></summary>

<p>
Take Google Sheets for example. Create a script under Editor folder, and copy below script content to it. The only need to focus or change is the order of alias/type/field. See the comments in code.

```csharp
/// <summary>
/// This class works on Yade 1.4.2+ 
/// </summary>
public class GoogleSheetsWithMetaImporter : GoogleSheetsImporter
{
    protected override int PreprocessingWithSkipRows(DataTable table, AppState state)
    {
        int metaInfoRowsCount = 3;
        var rowCount = table.Rows.Count;
        if (rowCount < metaInfoRowsCount)
        {
            return metaInfoRowsCount;
        }

        var columnCount = table.Columns.Count;
        HashSet<int> configedColumns = new HashSet<int>();

        // Change the indexes if your spread sheets meta schema is different.
        int aliasRowIndex = 0;
        int typeRowIndex = 1;
        int fieldRowIndex = 2;

        for (int columnIndex = 0; columnIndex < columnCount; columnIndex++)
        {
            var alias = table.Rows[aliasRowIndex].ItemArray[columnIndex].ToString();
            var typeString = table.Rows[typeRowIndex].ItemArray[columnIndex].ToString().ToLower();
            var field = table.Rows[fieldRowIndex].ItemArray[columnIndex].ToString();

            if (string.IsNullOrEmpty(alias) && string.IsNullOrEmpty(typeString) && string.IsNullOrEmpty(field))
            {
                continue;
            }

            if (string.IsNullOrEmpty(typeString))
            {
                typeString = "string";
            }

            int type = DataTypeMapper.NameToKey(typeString);
            state.data.SetColumnHeaderColumn(columnIndex, alias, type, field);
            configedColumns.Add(columnIndex);
        }

        var keys = state.data.columnHeaders.items.Keys;
        foreach (var key in keys)
        {
            if (configedColumns.Contains(key))
            {
                continue;
            }

            state.data.DeleteColumnHeaderSettings(key);
        }

        state.BindingSheet.UpdateColumnSettings();

        return metaInfoRowsCount;
    }

    public override string GetMenuName()
    {
        return "Import From Google Sheets (With Meta)";
    }
}

internal class GoogleSheetsWithMetaBulkImport : GoogleBulkImportMethod
{
    public override string GetName()
    {
        return "GoogleWithMeta";
    }

    protected override int PreprocessingWithSkipRows(DataTable table, YadeSheetData targetSheet)
    {
        int metaInfoRowsCount = 3;
        var rowCount = table.Rows.Count;
        if (rowCount < metaInfoRowsCount)
        {
            return metaInfoRowsCount;
        }

        var columnCount = table.Columns.Count;
        HashSet<int> configedColumns = new HashSet<int>();

        // Change the indexes if your spread sheets meta schema is different.
        int aliasRowIndex = 0;
        int typeRowIndex = 1;
        int fieldRowIndex = 2;

        for (int columnIndex = 0; columnIndex < columnCount; columnIndex++)
        {
            var alias = table.Rows[aliasRowIndex].ItemArray[columnIndex].ToString();
            var typeString = table.Rows[typeRowIndex].ItemArray[columnIndex].ToString().ToLower();
            var field = table.Rows[fieldRowIndex].ItemArray[columnIndex].ToString();

            if (string.IsNullOrEmpty(alias) && string.IsNullOrEmpty(typeString) && string.IsNullOrEmpty(field))
            {
                continue;
            }

            if (string.IsNullOrEmpty(typeString))
            {
                typeString = "string";
            }

            int type = DataTypeMapper.NameToKey(typeString);
            targetSheet.SetColumnHeaderColumn(columnIndex, alias, type, field);
            configedColumns.Add(columnIndex);
        }

        var keys = targetSheet.columnHeaders.items.Keys;
        foreach (var key in keys)
        {
            if (configedColumns.Contains(key))
            {
                continue;
            }

            targetSheet.DeleteColumnHeaderSettings(key);
        }

        return metaInfoRowsCount;
    }
}
```
</details>
