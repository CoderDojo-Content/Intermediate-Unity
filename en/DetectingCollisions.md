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
  
  **OnCollisionEnter()** is a built in function that is called when the object the script is attached to and another object collide. The if statement is to make sure that the projectile collided with an obstacle, then the two objects are destroyed.
  
3. Now you can detect a collision with an obstacle and the projectile, but not your "Player" object and an Obstacle. Add this code to your "Player" script

    ```csharp
    void OnCollisionEnter(Collision col)
    {
        if(col.gameObject.name == "obstacle(Clone)")
        {
            Destroy(gameObject);
            Destroy(col.gameObject);
        }
    }
    ```