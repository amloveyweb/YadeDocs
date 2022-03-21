# Binary Serialization

Binary Serialization APIs can serialize Yade sheet or Yade Database to byte array and deserialize them from bytes. We can save the byte array to disk or upload to web services which depends on project requirements. 

To enable the binary serialization feature, we need to set `BinarySerializerEnabled` property to `true`. For exampple:

```csharp
// Turn on yade sheet instance binary serialization feature
YadeSheetInstance.BinarySerializerEnabled = true;

// Turn on yade database binary serialization feature
YadeDatabaseInstance.BinarySerializerEnabled = true;

// or Use YadeDB Utilities
YadeDB.SetBinarySerializerEnabled(true, dbName);
```

### Binary Serialization Mode

Yade have two modes in binary serialization: **Full** and **Incremental**.

* **Full binary serialzation mode** will serialize all sheets data to bytes

* **Incremental binary serialization mode** only serialize **changes of data** to bytes. This is default behaviour of Yade

### Serialize and Deserialize

All of YadeSheetData, YadeDatabase and YadeDB Utilites have method called `Serialize()` and `Deserialize()`:

* `Serialize()`: to serialize data to bytes
* `Deserialize()`: to deserialize types to data

Below is a code samples:

```csharp
YadeSheetData sheet = ScriptableObject.CreateInstance<YadeSheetData>();
sheet.BinarySerializerEnabled = true;

sheet.SetRawValue("A1", "Hello");
sheet.SetRawValue(1, 0, "World!");

// Serialize data to binaries
byte[] bytes = sheet.Serialize();

// Deserialize binaries to data
sheet.Deserialize(bytes);
```
