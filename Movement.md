### Player with Rigidbody
```
#if UNITY_EDITOR
        mouse = Input.mousePosition;
        target = Camera.main.ScreenToWorldPoint(new Vector3(mouse.x, mouse.y, 10));
        rb.MovePosition(new Vector2(target.x,target.y));
#else
        void Update()
        {
            Touch touch = Input.GetTouch(0);

            if (touch.phase == TouchPhase.Began)
            {
                previousPos = Camera.main.ScreenToWorldPoint(touch.position);
            }
            if (touch.phase == TouchPhase.Moved)
            {
                currentPos = Camera.main.ScreenToWorldPoint(touch.position);
                diff_x = (currentPos.x - previousPos.x);
                diff_y = (currentPos.y - previousPos.y);

                rb.MovePosition(rb.position + new Vector2(diff_x,diff_y));

                previousPos = currentPos;
            }
            else
            {
                rb.velocity = Vector3.zero;
            }
        }
#endif
```
