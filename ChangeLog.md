# CHANGE LOG

### Version 1.4.1

**NEW:**
- Invalid formulas or invalid value of formulas will show as `#N/A`
- FlowCanvasIntegration.unitypackage included in package instead of downloading from web
- Add Help icon button on toolbar of spreadsheet editor

**IMPROVED:**
- Update help url for YadeSheetData and YadeDatabase class
- Combine Import and Export drop down to one

**FIXED:**
- Update BinarySerializationTest demo to make it works on WebGL

### Version 1.4.0

**NEW:**
- Add Binary Serialization support for YadeSheetData and YadeDatabase. These APIs are working when `BinarySerializerEnabled` property is set to true [Experimental]
- Add `Ctrl + S` on Windows and `Cmd + S` on macOS to save data manually

**IMPROVED:**
- Improve alpha based cell index to cell index performance by caching
- Improve that arrows keys and copy&paste shortcuts are works for for cell text input when editing cell data

**FIXED:**
- Fix bug that after cell updated, `YadeDB.Q<T>()` method return list that contains old data
- Fix bug that top cell edit not update value when data revert from version control software
- Fix bug that data added by SetRawValue methods keep exits after exiting play mode in Unity Editor

### Version 1.3.0

**NEW:**
- Add support for importing Google Sheets (public links)
- Add new API `SetRawValue()` to YadeSheetData, YadeDatabase and YadeDB Utilites class that able to set cell raw data
- Add `YadeDBSetCellRawValueByAlphaIndex` and `YadeDBSetCellRawValueByIndex` Playmaker actions
- Add Flow Canvas Visual Scripting support

**FIXED:**
- Fix bug that sheet names are not loaded when importing excel file with multiple sheets on Unity 2021.2+
- Fix bug that top cell text input hard to resize
- Fix bug that cannot resize headers after top cell text input resized
- Fix bug that config extra headers menu show even click wrong area above headers
- Fix bug that redo/undo can be executed even has popup window
- Fix auto fill range selection goes wrong after click auto fill element twice

### Version 1.2.0

**NEW:**
- Add YadeDatabase which access sheet data much easier.
- Add YadeDB Utilities to access sheet data more quicker and efficient
- Add ability that able to select sheet to import when importing excel

**FIXED:**
- Fix bug that cursor lost after insert formula sometime

### Version 1.1.0

**IMPROVED:**
- Improve supports of DBCS IME

**FIXED:**
- Fix blank cell not allow some characters (like mins) as first char
- Fix paste caction will clear the copied cell state
- Fix icons of Search Input are missing on Unity 2021.2

### Version 1.0.8

**NEW:**
- Add formula function `ENUM` to support enum type data, and it will show as dropdown list cell
- Add custom type support for `AsList` or `AsDictionary` method of YadeSheetData class.
- Add simple code generator for data class

**IMPROVED:**
- Improve column header settings to support filed and datat type settings which can used for code generation

**FIXED:**
- Fix resizer don't appear when hover on header edge in some scenario


### Version 1.0.7

- Unity 2021.2 compatibilty

### Version 1.0.6

**NEW:**
- Add Play Maker actions that able to set values of cell

**FIXED:**
- Fix bug that cell data copied form Excel may have `\r` in end of content of cell
- Fix bug that Yade editor cannot be opened after Yade folder is draged to Plugins folder

### Version 1.0.5

**NEW:**
- Add ability that Yade can be dragged to Plugins folder
- Add `AsList()` and `AsDictionary()` method to YadeSheetData class, please see the updated samples code in package

**IMPROVED:**
- Opened window will be cosed after sheet file deleted
- Improve integration with source version control software, like Git
- Update Yadesheet Inspector to not show scriptobject default UI when multiple yadesheet selected

**FIXED:**
- Fix resizer does not works in some scenarios

### Version 1.0.4

**NEW:**
- Add Search content feature
- Add Online document link
- Copy between multiple sheets are available now

**FIXED:**
- Fix double click header cell will enter edit mode bug
- Fix pressed 'Enter' in top cell editor will not update cell content bug

### Version 1.0.3 (thanks IcepOwer)

**FIXED:**
- Fix move selection bug
- Fix content will not update in some scenarios
- Fix bugs in int and alpha index converter

### Beta 3 (thanks IcepOwer)

**NEW:**
- Add more extension api to get value for more types for cell, for example `GetInt`, `GetFloat`. These methods are under `Yade.Runtime.Extensions` namespace
- Add Play Maker Support, see the `Yade Sheet` action category

**FIXED:**
- Fix bug that mins function are not work
- Fix bug that formula is not auto update after referenced cells are updated


### Beta 2

**NEW:**
- Add dark theme
- Add selection count in status bar