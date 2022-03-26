
# Getting Stared

Yade is easy to use. Let's following below steps to go through Yade features.

### 1. Create Sheet File

Right click in Project Window and select **Create -> Yade Sheet** Menu to create a yade sheet file. Let's name it `TestSheet`. Double click the sheet file to start editing.

### 2. Edit Sheet file

Double click the yadesheet file will open Spreadsheet Editor. Let's add some data to `A1` and `B1`.

| A | B |
|--|--|
|Hello | Samples|

### 3. Access Cell

Create a script named `Test.cs` in Unity Project Window and copy below content to the script.

```csharp
using UnityEngine;
using Yade.Runtime;

public class Test : MonoBehaviour
{
    public YadeSheetData sheet;

    void Start()
    {
        Debug.Log(sheet.GetCell(0, 0).GetValue());
        Debug.Log(sheet.GetCell("B1").GetValue());
    }
}

```

After save script content and script reimported. Drag the script to any GameObject in Hierachy Window. And then drag the yadesheet file to link the script variable.

Click play button, we should see `"Hello Samples"` will ouput to Unity Editor Console Window.

### 4. Deserialize sheet to C# objects

We also can deserialize sheet data to c# objects. First, we need creat a class, say it's name is `Data`. 

```csharp
public class Data
{
    [DataField(0)] public string A;
    [DataField(1)] public string B;
}
```

We use `DataField` attribute to bind field to sheet columns. And then, we can deserialize the sheet data like this:

```csharp
var list = sheet.AsList<Data>();
Debug.Log(list[0].A);
Debug.Log(list[0].B);
```

Output of above code is the same as section #3

We also can deserialize sheet data to dictionary like this:

```csharp
sheet.AsDictionary<string, Data>(item => item.A);
```

Above code will create a dictionary with first column as keys.

### 5. Use YadeDatabase

Create `Resources` folder if there are not exists. We right click folder and execute the menu **Create** -> **YadeDatabase**, will create a YadeDatabase asset with default name `YadeDB`.

Let's drag the yadesheet to the inspector of YadeDatabase asset.

### 6. Use YadeDB

Now we can access the data using YadeDB Utilites like:

```csharp
// The sheet name is TestSheet
YadeDB.Q("TestSheet", "A1").GetValue();
YadeDB.Q("TestSheet", 1, 0).GetValue();
```

### 7. Full Sample Code

We have use three ways to access sheet data, below is the full sample code:

```csharp
using UnityEngine;
using Yade.Runtime;

public class Test : MonoBehaviour
{
    public YadeSheetData sheet;

    public class Data
    {
        [DataField(0)] public string A;
        [DataField(1)] public string B;
    }

    void Start()
    {
        Debug.Log(sheet.GetCell(0, 0).GetValue());
        Debug.Log(sheet.GetCell("B1").GetValue());

        var list = sheet.AsList<Data>();
        Debug.Log(list[0].A);
        Debug.Log(list[0].B);
        
        Debug.Log(YadeDB.Q("TestSheet", "A1").GetValue());
        Debug.Log(YadeDB.Q("TestSheet", 1, 0).GetValue());
    }
}

```