1. Create a folder in your Assets folder and name it "Scripts". Now create a new C# script in your new "Scripts folder" and name it "Player".

2. Add this code to the **Update()** function. 
    ```csharp
Vector3 mousePos = Input.mousePosition;  

    mousePos.z = 15f;
    this.transform.position = Camera.main.ScreenToWorldPoint(mousePos);
    ```
    Now lets break down what this code does! 

    **Vector3**'s are structures (a structure stores multiple variables in one unit). Unity uses **Vector3** to keep track of an object's position in the world (x, y, z). So, when you set the **Vector3** equal to the **Input.mouseposition** the x and y values of the **Vector3** are changed each frame (because its in the update function).
    
     Notice **Input.mousePosition** doesn't change the **Vector3**'s position on the z-axis. You can set the z value by using "**.**" (called the "Dot Operator"). This allows us to access the variables within the **Vector3** structure.
     
     The last line moves our "player" object to the position of our mouse! "this" is a keyword that refers to the object the script is attached to. **transform.position** changes the location of the "this" (or your "Player") object. **Camera.main.ScreenToWorldPoint(mousePos)** sets the position of your "Player" object in the game world space.
     
3.  If you ran the game, did you notice that the "Player" object doesn't stay on the screen? You can fix this by adding this bit of code underneath the code you added in step 2!

```csharp
        Vector3 spritePos = Camera.main.WorldToViewportPoint(transform.position);
        spritePos.x = Mathf.Clamp(spritePos.x, 0.05f, 0.95f);
        spritePos.y = Mathf.Clamp(spritePos.y, 0.1f, 0.9f);
        transform.position = Camera.main.ViewportToWorldPoint(spritePos);
```