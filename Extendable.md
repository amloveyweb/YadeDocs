### Extend Yade

#### Add Fomula Function

Create a script file under **Editor** folder and create an class inhierted from class `FormulaFunction` . Below Sample code will create a function called `Hello` and it return fixed string `Supper man` .

```csharp
using Yade.Runtime.Formula;

public class Hello : FormulaFunction
{
    public override object Evalute()
    {
        return "Supper man";
    }

    public override string GetName()
    {
        return "HELLO";
    }
}

```

#### Add A Data Exporter

Create a script file under **Editor** folder and create an class inhierted from class `Exporter` . Below sample create a exporter menu named `Hello Exporter` .

```csharp
using Yade.Editor;

public class HelloExporter : Exporter
{
    public override bool Execute(AppState state)
    {
        // Do logic of exporter: read data from AppState.data and write to other files
        return true;
    }

    public override string GetMenuName()
    {
        return "Hello Exporter";
    }

    public override bool IsAvailable(AppState state)
    {
        return true;
    }
}
```

#### Add A Data Importer

Create a script file under **Editor** folder and create an class inhierted from class `Exporter` . Below sample create a exporter menu named `Hello Exporter` .

```csharp
using Yade.Editor;

public class HelloImporter : Importer
{
    public override bool Execute(AppState state)
    {
        // Do logic of importer: loading data from datasource and write them into AppState.data
        // If return result is true, yade will refresh ui after importing completed
        return true;
    }

    public override string GetMenuName()
    {
        return "Hello Importer";
    }

    public override bool IsAvailable(AppState state)
    {
        return true;
    }
}
```

#### Add Context Menu Item

To add an item to right click context menu of selected cells, create a script file under **Editor** folder and create an class inhierted from class `ContextMenuItem` . Below sample create a exporter menu named `AutoFillRandomNumber`.

```csharp
public class AutoFillRandomNumber : ContextMenuItem
{
    public override void Execute(AppState state)
    {
        var selectedRange = state.selectedRange;
        if (selectedRange != null)
        {
            selectedRange.ForEach((row, column) =>
            {
                state.SetCellRawValue(row, column, Random.Range(int.MinValue, int.MaxValue).ToString());
            });

            state.BindingSheet.UpdateUIBaseOnState();
        }
    }

    public override bool GetEnabledState(AppState state)
    {
        var selectedRange = state.selectedRange;
        if (selectedRange == null)
        {
            return false;
        }

        if (selectedRange.IsWholeColumn() || selectedRange.IsWholeRow())
        {
            return false;
        }

        return true;
    }

    public override string GetMenuKey()
    {
        return "FillRandomNumber";
    }

    public override string GetMenuName()
    {
        return "Auo Fill Random Number";
    }

    public override bool IsAvailable(AppState state)
    {
        return true;
    }
}
```