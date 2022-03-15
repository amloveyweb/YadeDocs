# CHANGE LOG

## Version 1.3.0

- Add support for importing Google Sheets (public links)
- Add new API `SetRawValue()` to YadeSheetData, YadeDatabase and YadeDB Utilites class that able to set cell raw data
- Add `YadeDBSetCellRawValueByAlphaIndex` and `YadeDBSetCellRawValueByIndex` Playmaker actions
- Add Flow Canvas Visual Scripting support
- Fix bug that sheet names are not loaded when importing excel file with multiple sheets on Unity 2021.2+
- Fix bug that top cell text input hard to resize
- Fix bug that cannot resize headers after top cell text input resized
- Fix bug that config extra headers menu show even click wrong area above headers
- Fix bug that redo/undo can be executed even has popup window
- Fix auto fill range selection goes wrong after click auto fill element twice

## Version 1.2.0

- Add YadeDatabase which access sheet data much easier.
- Add YadeDB Utilities to access sheet data more quicker and efficient
- Add ability that able to select sheet to import when importing excel
- Fix bug that cursor lost after insert formula sometime

## Version 1.1.0

- Improve supports of DBCS IME
- Fix blank cell not allow some characters (like mins) as first char
- Fix paste caction will clear the copied cell state
- Fix icons of Search Input are missing on Unity 2021.2

## Version 1.0.8

- Add formula function `ENUM` to support enum type data, and it will show as dropdown list cell
- Add custom type support for `AsList` or `AsDictionary` method of YadeSheetData class.
- Add simple code generator for data class
- Improve column header settings to support filed and datat type settings which can used for code generation
- Fix resizer don't appear when hover on header edge in some scenario


## Version 1.0.7

- Unity 2021.2 compatibilty

## Version 1.0.6

- Add Play Maker actions that able to set values of cell
- Fix bug that cell data copied form Excel may have `\r` in end of content of cell
- Fix bug that Yade editor cannot be opened after Yade folder is draged to Plugins folder

## Version 1.0.5

- Add ability that Yade can be dragged to Plugins folder
- Add `AsList()` and `AsDictionary()` method to YadeSheetData class, please see the updated samples code in package
- Opened window will be cosed after sheet file deleted
- Improve integration with source version control software, like Git
- Update Yadesheet Inspector to not show scriptobject default UI when multiple yadesheet selected
- Fix resizer does not works in some scenarios

## Version 1.0.4

- Add Search content feature
- Add Online document link
- Copy between multiple sheets are available now
- Fix double click header cell will enter edit mode bug
- Fix pressed 'Enter' in top cell editor will not update cell content bug

## Version 1.0.3 (thanks IcepOwer)

- Fix move selection bug
- Fix content will not update in some scenarios
- Fix bugs in int and alpha index converter

## Beta 3 (thanks IcepOwer)

- Add more extension api to get value for more types for cell, for example `GetInt`, `GetFloat`. These methods are under `Yade.Runtime.Extensions` namespace
- Add Play Maker Support, see the `Yade Sheet` action category
- Fix bug that mins function are not work
- Fix bug that formula is not auto update after referenced cells are updated


## Beta 2

- Add dark theme
- Add selection count in status bar