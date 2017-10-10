1. You have all the components of your game working now! Awesome, but... they don't do anything when they collide. Colliding is when two objects touch each other. You need to detect the collision between the game's objects and write a script that does something when that collision is detected.

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
  
  **OnCollisionEnter()** is a built in function that is called when the object the script is attached to and another object collide. Within this function you have two **GameObjects** `col.gameObject` and `gameObject`. `gameObject` is what the script is attached to (the laser clone) and `col.gameOBject` is the thing colliding with the laser (the asteroid). `col.gameobject.name` returns the name of the object the laser collided with. The `if` statement is to make sure that if the laser collided with an asteroid (which will be called Asteroid(Clone)), then the two objects will be destroyed. 
  
3. Since you're destroying asteroids, you could make it play a sound! Create an **Empty** (**GameObject > Create Empty**) and call it "AsteroidExplosion". Add an **AudioSource** component to the Empty. Open up the "Audio" Assets folder and drag and drop the "DestroyAsteroidSound" sound into the "AsteroidExplosion" **Inspector** for "Audio Clip". Finally, uncheck the "Play On Awake" property. 

4. To play the **AudioSource** some code needs to be added into the `if` statement you made in the last step.

    ```csharp
    AudioSource audio = GameObject.Find("AsteroidExplosion").GetComponent<AudioSource>();
    audio.Play();
    ```
    
    This code finds the game object you made with the first line. The second line plays the sound that you added to the **AudioSource**.
    
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
    Do you know what the `gameObject` is here? It is your "Player" object because your script is attached to the "Player" object. That means the `col.gameObject` is an asteroid.
    
6. Let's play a different noise if the player collides with an asteroid. Create another **Empty** and call it "DestroyPlayerSound". Add an **AudioSource** and add the "explosion_player" sound to it. Finally, add this code to the **OnCollisionEnter()** function in the "Player" script.

    ```csharp
    AudioSource audio = GameObject.Find("DestroyPlayerSound").GetComponent<AudioSource>();
    audio.Play();
    ```
   
7. Try shooting after you run into an asteroid! 
You have detected collisions between all of the objects in your game, but did you notice the bug? If you have the time after you finish these Sushi Cards you can try to fix the bug!

    
    