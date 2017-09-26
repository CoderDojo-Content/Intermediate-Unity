1. You have all the components of your gaming working now! Awesome, but... they don't do anything when they collide. You need to detect the collision between the objects and write a script that handles that condition.

2. Create a new C# script called "projectileClone". Add the following code to the script.

  ```csharp
  public class laserClone : MonoBehaviour
  {
    public void OnCollisionEnter(Collision col)
    {
      if (col.gameObject.name == "obstacle(Clone)")
      {
        // Destroy both objects
        Destroy(col.gameObject);
        Destroy(gameObject);
      }
    }
  ```
  
  