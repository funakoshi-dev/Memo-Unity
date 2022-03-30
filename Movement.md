### Player with Rigidbody
```
#if UNITY_EDITOR
        mouse = Input.mousePosition;
        target = Camera.main.ScreenToWorldPoint(new Vector3(mouse.x, mouse.y, 10));
        rb.MovePosition(new Vector2(target.x,target.y));
#else
        if (0 < Input.touchCount)
        {
            Touch touchPos = Input.GetTouch(0);

            if (TouchPhase.Moved == touchPos.phase)
            {
                Vector2 moveDist = (touchPos.deltaPosition / touchPos.deltaTime) * Time.deltaTime;
                rb.velocity = new Vector3(moveDist.x, moveDist.y, 0);
            }
        }
        else
        {
            rb.velocity = Vector3.zero;
        }
#endif
```
