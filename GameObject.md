
### Change GameObject to show
```
public void ActivatePanel(string nextPanel)
{
    firstPanel.SetActive(nextPanel.Equals(firstPanel.name));
    secondPanel.SetActive(nextPanel.Equals(secondPanel.name));
}
```

### Switch GameObject On/Off
```
public void SwitchActiveState()
{
    testObject.SetActive(!testObject.activeSelf);
}
```

### Move GameObject Front or Back
```
GetComponent<RectTransform>().SetAsLastSibling(); //Front
GetComponent<RectTransform>().SetAsFirstSibling(); //Back
```

# Resize / Relocation
## Example
### Wall to screen edge
```
public class Wall : MonoBehaviour
{
    [SerializeField] Camera _camera;
    [SerializeField] GameObject wall_left;
    [SerializeField] GameObject wall_right;
    [SerializeField] GameObject wall_top;
    [SerializeField] GameObject wall_bottom;
    Vector3 screen_LeftBottom;
    Vector3 screen_RightTop;

    void Start()
    {
        // Set layer for physics collision detection
        wall_left.layer = LayerMask.NameToLayer("Wall");
        wall_right.layer = LayerMask.NameToLayer("Wall");
        wall_top.layer = LayerMask.NameToLayer("Wall");
        wall_bottom.layer = LayerMask.NameToLayer("Wall");

        MoveWallToEdge();

        ResizeWall();
    }

    void MoveWallToEdge()
    {
        screen_LeftBottom = Camera.main.ScreenToWorldPoint(Vector3.zero);
        screen_RightTop = Camera.main.ScreenToWorldPoint(new Vector3(Screen.width, Screen.height, 0));

        wall_left.transform.position = new Vector3(screen_LeftBottom.x, 0, 0);
        wall_right.transform.position = new Vector3(screen_RightTop.x, 0, 0);
        wall_top.transform.position = new Vector3(0, screen_RightTop.y, 0);
        wall_bottom.transform.position = new Vector3(0, screen_LeftBottom.y, 0);
    }

    void ResizeWall()
    {
        float height = _camera.orthographicSize * 2f;
        float screenRatio = (float)Screen.width / (float)Screen.height;
        float width = screenRatio * height;

        wall_right.transform.localScale = new Vector3(0.5f, height, 1);
        wall_left.transform.localScale = new Vector3(0.5f, height, 1);
        wall_top.transform.localScale = new Vector3(width, 0.5f, 1);
        wall_bottom.transform.localScale = new Vector3(width, 0.5f, 1);
    }
}
```
