1. Now let's create something to destroy the asteroids. In game programming and physics a **projectile** is an object that is cast (thrown, fired, moved) from one place to another and **gravity** affects it. So, when a football player kicks the ball, in physics, the ball would become a projectile once it starts moving.

2. Create a new C# script called "lasers" (make sure its in the "Scripts" folder) and attach it to the empty "Lasers" object you made earlier.

3.  Inside your "lasers" script, replace the code inside your lasers class with this code.
    
    ```csharp
    public float laserSpeed = 20f;
    public GameObject laser;
    
    void Update(){
      if (Input.GetMouseButtonDown(0))
      {
        Vector3 pos;
        pos.x = 0;
        pos.y = 0;
        pos.z = 0;
        // Create a laser clone
        GameObject laserClone = Instantiate(laser, pos, transform.rotation) as GameObject; 
        //Add a Rigidbody to the clone and move it
        Rigidbody laserCloneRB = laserClone.GetComponent<Rigidbody>();
        laserCloneRB.velocity = transform.up * laserSepeed;
        // Destroy clone if alive too long
        Destroy(laserClone, 2.5f);
      }
    }
    ```
    
    Notice this looks similar to the obstacle that you just created. You've added an `if` statement so that this block of code only runs when the player left clicks. 
    
    * You can find other input options here: [dojo.soy/Input](https://docs.unity3d.com/ScriptReference/Input.html). If you want, try to allow the player to fire a laser when they press a different button like the spacebar.
    
    
4. That almost works, but if you run the game you will see that the laser doesn't come from the player. Remember the code we used in the "Player: script to find where the mouse location is? You will use the same logic so the game knows where to fire a laser from. Add this code to your "lasers" script:

    ```csharp
    Vector3 mousePos = Input.mousePosition;
    mousePos.z = 15f;
    mousePos = Camera.main.ScreenToWorldPoint(mousePos);
    // Make laser come from front of player
    mousePos.y += 1f;
    ```
    This code looks similar to the "Player" script, but you might have not seen this operator before `mousePos.y += 1f;`. Coders are pretty lazy and using these "shorthand" operators allow us to shorten code. `a += b` is the same as ` a = a + b`, but notice how much shorter the first one is! Here is a list of the shorthand operators in C#: [dojo.soy/C#ShorthandOperators](https://en.wikibooks.org/wiki/C_Sharp_Programming/Operators#Short-hand_Assignment).

    Finally, replace the `pos` in the **Instantiate()** function with `mousePos`
    
    ```csharp
    GameObject laserClone = Instantiate(laser, pos, transform.rotation) as GameObject;
    ```
    with
    ```csharp
    GameObject laserClone = Instantiate(laser, mousePos, transform.rotation) as GameObject;
    ```
    
5. Lasers make sounds too! Let's add a sound to this laser. Click on the laser in the "Prefabs" folder and add an **AudioSource** component (**Component > Audio > Audio Source**). From the "Audio" folder drag "LaserSound" into the **Audio Clip** property in the "Laser" prefab **Inspector**.

    If you run the game you can test the lasers out!
