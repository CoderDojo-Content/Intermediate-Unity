1. Create a folder in your Assets folder and name it "Scripts". Now create a new C# script in your new "Scripts folder" and name it "Player".
2. Add this code to the **Update()** function. 

    ```csharp
    Vector3 mousePos = Input.mousePosition;  
    mousePos.z = 15f;
    this.transform.position = Camera.main.ScreenToWorldPoint(mousePos);
    ```
3.  