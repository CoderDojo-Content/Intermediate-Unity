1. Create a new folder called "Lasers" (make sure its in the "Scripts" folder). Now create three C# scripts:  "CreateLasers", "MoveLaser", and "DestoryLaser".

2. Start with creating a laser. Attach the "CreateLasers" script to the "Lasers" **GameObject**. Add this code: 
    
    ```csharp
    public GameObject laser;
    
    void Update(){
      if (Input.GetMouseButtonDown(0))
      {
        Vector3 createPosition = player.transform.location;
        createPosition.y += 1f;
        // Create a laser clone
        GameObject laserClone = Instantiate(laser, pos, transform.rotation) as GameObject; 
      }
    }
    ```
    
    Now, just attach the laser prefab to the script.
    
    Notice this looks similar to the obstacle that you just created. You've added an `if` statement so that this block of code only runs when the player left clicks.

    `player.transform.location` is the center of the player **GameObject**. 
    
    You don't wan't to create the laser inside of the spaceship so adding 1 to the y value will stop that. 
    
    You might not of seen this operator before `pos.y += 1f;`. Coders are pretty lazy and using these "shorthand" operators allow us to shorten code. `a += b` is the same as ` a = a + b`, but notice how much shorter the first one is! Here is a list of the shorthand operators in C#: [dojo.soy/C#ShorthandOperators](https://en.wikibooks.org/wiki/C_Sharp_Programming/Operators#Short-hand_Assignment).
    
    [Note]: You can find other input options here: [dojo.soy/Input](https://docs.unity3d.com/ScriptReference/Input.html). If you want, try to allow the player to fire a laser when they press a different button like the spacebar.
    
3. 
    
5. Lasers make sounds! Lets add a sound to this laser. Click on the laser in the "Prefabs" folder and add an **AudioSource** component (**Component > Audio > Audio Source**). From the "Audio" folder drag "LaserSound" into the **Audio Clip** property in the "Laser" prefab **Inspector**.

    If you run the game you can test the lasers out!
