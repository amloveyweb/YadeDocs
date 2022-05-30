# Get Online Sheet Data 

Yade support two types of online sheet data: **CSV** and **Google Sheets** (public share link).

For the usage, below is a code sample

```csharp
public IEnumerator GetSheetDataFromGoogleSheets()
{
    var url = "https://docs.google.com/spreadsheets/d/1TOKg3YghXYLyxtaduC0r6q1bqUYoVLfPW8X7zR-WwkY/edit?usp=sharing";
    
    // Download data from Google Sheets, 41631710 is the sheet id of the 
    // Google Sheet. If no sheet id (gid) specific, the first sheet will
    // be downloaded
    var os = new OnlineGoogleSheet(url, "41631710");
    yield return os.DownloadSheetData();

    // Get YadeSheet
    var sheet = os.GetYadeSheetData();
}
```

After get YadeSheetData instance, we can use [Binary Serialization](BinarySerialization.md#binary-serialization) to save data to local or update another sheet by [`YadeSheetData.CopyTo`](YadeSheetData.md#code-samples) method. Below is sample for save to local by BinarySerialization:

```csharp
public IEnumerator GetSheetDataFromGoogleSheetsAndSaveToLocal()
{
    var url = "https://docs.google.com/spreadsheets/d/1TOKg3YghXYLyxtaduC0r6q1bqUYoVLfPW8X7zR-WwkY/edit?usp=sharing";
    
    // Download data from Google Sheets, 41631710 is the sheet id of the 
    // Google Sheet. If no sheet id (gid) specific, the first sheet will
    // be downloaded
    var os = new OnlineGoogleSheet(url, "41631710");
    yield return os.DownloadSheetData();

    // Get YadeSheet
    var sheet = os.GetYadeSheetData();

    // Save To local, We need to use full serialization mode here
    sheet.BinarySerializerEnabled = true;
    var settings = new BinarySerializationSettings();
    settings.Mode = BinarySerializationMode.Full;
    var data = sheet.Serialize(settings);
    File.WriteAllBytes(localFilePath, data);
}
```

