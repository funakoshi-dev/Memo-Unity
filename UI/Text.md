## Text Blinker
```
public class TextBlinker : MonoBehaviour
{
    Text text;
    public float speed = 1;
    float delta;

    void Start()
    {
        text = this.gameObject.GetComponent<Text>();
    }

    void Update()
    {
        text.color = GetAlphaColor(text.color);
    }

    Color GetAlphaColor(Color color)
    {
        delta += Time.deltaTime * speed;
        color.a = Mathf.Sin(delta);
        return color;
    }
}
```
