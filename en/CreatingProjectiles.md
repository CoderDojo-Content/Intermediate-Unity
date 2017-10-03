1. Now lets create something to destroy the asteroids. In game programming and physics a **projectile** is an object that is cast from one place to another. So, when a football/Soccer player kicks the ball, in physics, the ball would become a projectile once it starts moving.

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
    
    Notice this looks similar to the obstacle that you just created. You've added an if statement so that this block of code only runs when the player left clicks. (You can find other input options here. [dojo.soy/Input](https://docs.unity3d.com/ScriptReference/Input.html). -(challenge fire on space)-
    
4. That almost works, but if you ran the game you noticed that the laser didn't come from the player. What code have you used to find where the mouse location is? Add this code to your "lasers" script

    ```csharp
    Vector3 mousePos = Input.mousePosition;
    mousePos.z = 15f;
    mousePos = Camera.main.ScreenToWorldPoint(mousePos);
    // Make laser come from front of player
    mousePos.y += 1f;
    ```
    We saw this code when we made the player move. (You might need to change the last line so your laser comes from the right location.)
    
    Finally, replace the "pos" in the **Instantiate()** function with "mousePos"
    
    ```csharp
    GameObject laserClone = Instantiate(laser, pos, transform.rotation) as GameObject;
    ```
    with
    ```csharp
    GameObject laserClone = Instantiate(laser, mousePos, transform.rotation) as GameObject;
    ```
    
5. Lasers make sounds! lets add a sound to this laser. Click on the laser in the "Prefabs" folder and add an "AudioSource" component (**Component > Audio > Audio Source**). From the "Audio" folder drag "laser_Sound" into the **Audio Clip** property in the "Laser" prefab **Inspector**.