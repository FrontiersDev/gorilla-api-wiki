# C# / Modding Integration

If you are developing a mod for Gorilla Tag (using BepInEx), you can fetch cosmetic data from this API to load custom assets or price lists dynamically.

## JSON Class
First, define a class to match the API response.

```csharp
[Serializable]
public class CosmeticItem
{
    public string id;
    public string name;
    public string slot;
    public int price;
    public ItemFiles files;
}

[Serializable]
public class ItemFiles
{
    public string icon;
    public string model;
}

[Serializable]
public class ApiResponse
{
    public CosmeticItem[] items;
}
```

```csharp
using System.Collections;
using UnityEngine;
using UnityEngine.Networking;
using Newtonsoft.Json;

public class ApiFetcher : MonoBehaviour
{
    private string apiUrl = "http://localhost:3000/api/cosmetics";

    void Start()
    {
        StartCoroutine(GetCosmetics());
    }

    IEnumerator GetCosmetics()
    {
        using (UnityWebRequest webRequest = UnityWebRequest.Get(apiUrl))
        {
            yield return webRequest.SendWebRequest();

            if (webRequest.result == UnityWebRequest.Result.Success)
            {
                string json = webRequest.downloadHandler.text;
                
                // Deserialize
                ApiResponse response = JsonConvert.DeserializeObject<ApiResponse>(json);
                
                foreach (var item in response.items)
                {
                    Debug.Log($"Found Item: {item.name} - {item.price} Rocks");
                }
            }
            else
            {
                Debug.LogError("API Error: " + webRequest.error);
            }
        }
    }
}
```