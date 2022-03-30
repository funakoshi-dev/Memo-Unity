## Example
```
using UnityEngine;

public class Data
{
    static int exp;

    static void LoadExp()
    {
        if (PlayerPrefs.HasKey("Exp"))
        {
            exp = PlayerPrefs.GetInt("Exp", 0);
        }
    }

    static void SaveExp()
    {
        PlayerPrefs.SetInt("Exp", exp);
    }

    public static int GetExp()
    {
        LoadExp();
        return exp;
    }

    public static void UpdateExp(int _exp)
    {
        exp = _exp;
        SaveExp();
    }
}
```
