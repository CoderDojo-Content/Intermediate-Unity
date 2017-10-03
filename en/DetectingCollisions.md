1. You have all the components of your gaming working now! Awesome, but... they don't do anything when they collide. You need to detect the collision between the objects and write a script that handles that condition.

2. Create a new C# script called "laserClone". Add the following code to the script.

  ```csharp
    public void OnCollisionEnter(Collision col)
    {
      if (col.gameObject.name == "Asteroid(Clone)")
      {
        // Destroy both objects
        Destroy(col.gameObject);
        Destroy(gameObject);
      }
    }
  ```
  
  **OnCollisionEnter()** is a built in function that is called when the object the script is attached to and another object collide. **col.gameobject.name** returns the name of the object the laser collided with. The if statement is to make sure that the laser collided with an asteroid (which will be called Asteroid(Clone)), then the two objects will be destroyed. 
  
3. Since you're destroying asteroids, you should make it play a sound! Create a **AudioSource** (**GameObject > Audio > AudioSource**) and call it "DestroyAsteroidSound". Open up the "Audio" Assets folder and drag and drop the sound into the "DestroyAsteroidSound" **Inspector** for "Audio Clip".

4. To play the **AudioSource** some code needs to be added into the if statement you made in the last step.

    ```csharp
    AudioSource audio = GameObject.Find("DestroyAsteroidSound").GetComponent<AudioSource>();
    audio.Play();
    ```

5. Now you can detect a collision with an asteroid and the laser, but not your "Player" object and an asteroid. Add this code to your "Player" script

    ```csharp
    void OnCollisionEnter(Collision col)
    {
        if(col.gameObject.name == "Asteroid(Clone)")
        {
            Destroy(gameObject);
            Destroy(col.gameObject);
        }
    }
    ```
    
6. Now you have detected collisions between all of the objects in your game. You might have noticed a bug after the player is destroyed! If you have the time after you finish you can try to fix the bug!

    