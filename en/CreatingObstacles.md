1. Create a new C# script in the "Scripts" folder named "Asteroids" and Attach it to the "Ateroids" **GameObject** you created earlier.

2. Add this code to you "Asteroids" script:

  ```csharp
  public GameObject asteroid;
  public float asteroidSpeed = 2f;
   
  void Update()
  {
    // Creating clones
    Vector3 spawnPosition;
    spawnPosition.x = 0;
    spawnPosition.y = 0;
    spawnPosition.z = 0;
    GameObject asteroidClone = Instantiate(asteroid, spawnPosition, asteroid.transform.rotation) as GameObject;
    // Move clones
    Rigidbody asteroidCloneRB = asteroidClone.GetComponent<Rigidbody>();
    asteroidCloneRB.velocity = -(transform.up * asteroidSpeed);
    // Make sure clone is destroyed
    Destroy(AsteroidClone, 10f);
  }
  ```
  
  To understand what's happening here you need to know what **instantiate** means. Instantiating something is creating a copy of a template. The template is the first object you pass into the **Instantiate()** function. In your case it is a **GameObject**! However, when you instantiate an object you must **Destroy()** it or your computer will slow down! The last line of this code destroys the instantiated object after 10 seconds. To make your asteroids move at a constant velocity you change the **Rigidbody**'s **velocity** property.
  
  Drag the Asteroid prefab you made and drop it into the "asteroid" box for your "asteroids" script in the **Inspector** for your "Asteroids" object. Try running your game.
  
4. WOAH! That was a lot of asteroids spawning! When you're repeatedly spawning an asteroid, you want to be able to control how fast it spawns. To do that you can use Unity's built in function **InvokeRepeating**! Add this to your code above **Update()**.

    ```csharp
    public float spawnTime = 1f;
    
    // Use this for initialization
    void Start()
    {
    // 0f is when to start invoking repeat
    InvokeRepeating("spawnAsteroid", 0f, spawnTime);
    }
    ```
    
    Now change `Update()` to `spawnAsteroid()`.
    
5. Now your asteroids spawn at a reasonable speed, but they only spawn in the same location. Lets make it more fun by spawning them at different locations every spawn. You can make a function that returns a random position to do this!
  
    ```csharp
    Vector3 randomSpawn()
    {
        float xPos = Random.Range(.5f, 9.5f);
        xPos = xPos / 10f;
        Vector3 spawnPosition = Camera.main.ViewportToWorldPoint(new Vector3(xPos, 1.1f, 15f));
        return spawnPosition;
    }
    ```
    
    Also remove these lines:
    
    ```csharp
    spawnPosition.x = 0;
    spawnPosition.y = 0;
    spawnPosition.z = 0;
    ```
    
    Finally, change `Vector3 spawnPosition;` to ` Vector3 spawnPosition = randomSpawn();`. 
    
    Putting **Vector3** instead of **void** in front of a function declaration means that the function well return a **Vector3** object. **Random.Range()** returns a random number between the two numbers given in the parameters. That number is then divided by 10 so that we get a number between 1 and 0, or the camera's viewport dimensions. You then create a **Vector3** to return called "spawnPosition". and set the "spawnPosition" to (our randomly generated x position, a y position that is off the screen, the z position that is level with your player object).