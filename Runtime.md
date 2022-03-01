# Yade Runtime

Yade Runtime supports all platforms that support ScriptableObject.

### Access Sheet

We can use [YadeSheetData](API.md#yadesheetdata) class to access the sheet data. Use the method `GetCell` to directly access data or deserialize the data to C# objects using `AsList<T>` or `AsDictionary<T>` extension methods.

### Deserializer

Unity Objects and primitive types are supported by deseralizer. If you have custom class type, implements the `ICellParser` interface can supported by Yade deserializer.

#### Support Custom Data Type

Class that implements `ICellParser` interface can support by deserializer.

```csharp
/// <summary>
/// Custom data type implement ICellParser which can support by AsList() method of YadeSheetData.
/// If it also has TypeKey attribute, it will show in dropdown menu of type header in Column Header
/// Settings Window of YadeEditor
/// </summary>
[TypeKey(10002)]
public class NumberData : ICellParser
{
    public int index;
    public int year;

    public void ParseFrom(string s)
    {
        var temp = s.Split(new char[] { ',' }, System.StringSplitOptions.RemoveEmptyEntries);
        if (temp.Length == 2)
        {
            index = int.Parse(temp[0]);
            year = int.Parse(temp[1]);
        }
    }
}
```

### YadeDatabase

[YadeDatabase](API.md#yadedatabase) is a group of Sheets, it provide more effective methods to query data of sheets.

[YadeDB](API.md#yadedb) is the Utilites class for YadeDataBase.