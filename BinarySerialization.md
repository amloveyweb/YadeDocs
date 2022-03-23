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

### Online Samples

[HERE](https://www.amlovey.com/YadeDocs/BS/index.html) is are online samples. Below is the code of the samples:

```csharp
public class BinarySerializationTest : MonoBehaviour
{
    public Text nameText;
    public RectTransform content;
    public GameObject itemPrefab;
    public InputField firstNameText;
    public InputField lastNameText;
    public Button addButton;

    private string dbName = "YadeSampleDB";
    private string sheetName = "Roles";

    public bool SerializationEnable = true;

    private class Role
    {
        [DataField(0)] public string FirstName;
        [DataField(1)] public string LastName;
    }

    void Start()
    {
        YadeDB.SetBinarySerializerEnabled(SerializationEnable, dbName);

        if (SerializationEnable)
        {
            string data = PlayerPrefs.GetString(dbName);
            if (!string.IsNullOrEmpty(data))
            {
                var bytes = Convert.FromBase64String(data);
                YadeDB.Deserialize(bytes, dbName);
            }
        }

        LoadList();

        addButton.onClick.AddListener(AddOne);
    }

    private void AddOne()
    {
        if (string.IsNullOrEmpty(firstNameText.text) || string.IsNullOrEmpty(lastNameText.text))
        {
            Debug.LogError("First Name and Last Name cannot be empty");
            return;
        }

        var rowCount = YadeDB.GetDatabase(dbName).Sheets[sheetName].GetRowCount();
        YadeDB.SetRawValue(sheetName, rowCount, 0, firstNameText.text, dbName);
        YadeDB.SetRawValue(sheetName, rowCount, 1, lastNameText.text, dbName);

        AddRoleToList(firstNameText.text, lastNameText.text);
        firstNameText.text = string.Empty;
        lastNameText.text = string.Empty;

        var scroll = content.GetComponentInParent<ScrollRect>();
        scroll.normalizedPosition = Vector2.up;

        var bytes = YadeDB.Serialize(dbName);
        PlayerPrefs.SetString(dbName, Convert.ToBase64String(bytes));
        PlayerPrefs.Save();
    }

    private void LoadList()
    {
        var roles = YadeDB.Q<Role>(sheetName, null, dbName);
        foreach (var role in roles)
        {
            AddRoleToList(role.FirstName, role.LastName);
        }
    }

    private void AddRoleToList(string firstName, string lastName)
    {
        var go = GameObject.Instantiate(itemPrefab);
        go.transform.SetParent(content);
        go.transform.SetAsFirstSibling();
        go.transform.localScale = Vector3.one;
        go.SetActive(true);

        var roleName = string.Format("{0}  {1}", firstName, lastName);
        var textComponent = go.transform.Find("Text").GetComponent<Text>();
        if (textComponent)
        {
            textComponent.text = roleName;
        }

        var btn = go.GetComponent<Button>();
        btn.onClick.AddListener(() =>
        {
            OnItemClick(roleName);
        });
    }

    private void OnItemClick(string roleName)
    {
        nameText.text = roleName;
    }
}
```