1. Now lets create something to destroy the obstacles. In game programming and physics a **projectile** is an object that is cast from one place to another. So, when a football player kicks the ball, in physics, the ball would become a projectile. Create your own projectile now in the scene (maybe a sphere or a rectangle) and add a rigidbody (uncheck **Use Gravity). Now make it into a prefab. (Remember to delete the old object from the scene!)

2. Create a new C# script called "projectiles" (make sure its in the "Scripts" folder) and attach it to the empty "Projectiles" object you made earlier.

3.  Inside your "projectiles" script, replace the code inside your projectiles class with this code.
    
    ```csharp
    public float projectileSpeed = 20f;
    public GameObject projectile;
    
    void Update(){
      if (Input.GetMouseButtonDown(0))
      {
        Vector3 pos;
        pos.x = 0;
        pos.y = 0;
        pos.z = 0;
        // Create projectile clone
        GameObject projectileClone = Instantiate(projectile, pos, transform.rotation) as GameObject; 
        //Add a Rigidbody to the clone and move it
        Rigidbody projectileCloneRB = projectileClone.GetComponent<Rigidbody>();
        projectileCloneRB.velocity = transform.up * projectileSpeed;
        // Destroy clone if alive too long
        Destroy(projectileClone, 2.5f);
      }
    }
    ```
    
    Notice this looks similar to the obstacle that you just created. You've added an if statement so that this block of code only runs when the player left clicks. (You can find other input options here. [dojo.soy/Input](https://docs.unity3d.com/ScriptReference/Input.html). -(challenge fire on space)-
    
4. That almost works, but if you ran the game you noticed that the projectile didn't come from the player. What code have you used to find where the mouse location is? Add this code to your "projectiles" script