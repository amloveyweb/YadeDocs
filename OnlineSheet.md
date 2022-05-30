# Online Sheet

Two types of online sheet for now: `OnlineCSVSheet` and `OnlineGoogleSheet`


### OnlineCSVSheet

Download data form online CSV content and parse to Yade Sheet.

#### Public Methods

|Name| Description|
|---|---|
DownloadSheetData | Download data form web |
GetYadeSheetData | Parse data to Yade Sheet|

#### Code Samples

```csharp
var url = "https://www.amlovey.com/uas/YadeTest.csv";
var onlineSheet = new OnlineCSVSheet(url);
yield return onlineSheet.DownloadSheetData();
var sheet = onlineSheet.GetYadeSheetData();
```

### OnlineGoogleSheet

Download data from Google Sheet (public share link) and parse to Yade Sheet.

#### Public Methods

|Name| Description|
|---|---|
DownloadSheetData | Download data form web |
GetYadeSheetData | Parse data to Yade Sheet|

#### Code Samples

```csharp
var url = "https://docs.google.com/spreadsheets/d/1TOKg3YghXYLyxtaduC0r6q1bqUYoVLfPW8X7zR-WwkY/edit?usp=sharing";
var os = new OnlineGoogleSheet(url);
yield return os.DownloadSheetData();
var sheet = os.GetYadeSheetData();
```