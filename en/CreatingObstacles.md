1. You'll use a few scripts for your asteroids, so to keep organized it's a good idea to make an "Asteroids" folder. Now, you will need 3 new C# scripts: CreateAsteroids, MoveAsteroid, and DestroyAsteroid.

2. Attach the "CreateAsteroids" script to  "CreateAsteroids" and add this code:

  ```csharp
  public GameObject asteroid;
   
  void Update()
  {
    Vector3 spawnPosition = Vector3.zero;
    GameObject asteroidClone = Instantiate(asteroid, spawnPosition, asteroid.transform.rotation) as GameObject;
  }
  ```
  To understand what's happening here you need to know what **instantiate** means. **Instantiating** something is like building something from plans or instructions. If you're baking a cake, the cake is the **instance** and the recipe is the **Instantiate()** function. In the game world, your cake is instead a **GameObject**!

  Drag the Asteroid prefab form the "Prefabs" folder and drop it into the "asteroid" box for your "CreateAsteroids" script in the **Inspector** for your "Asteroids" object. Try running your game.

3. WOAH! That was a lot of asteroids being created!The **Update()** function happens really fast so a lot of asteroids spawn. You can control how fast the asteroids are created with the `InvokeRepeating()` function. Add this to your previous code:

    ```csharp
    public float spawnTime = 1f;
    
    // Use this for initialization
    void Start()
    {
    // 0f is when to start invoking repeat
    InvokeRepeating("spawnAsteroid", 0f, spawnTime);
    }
    ```
    
    Now change `Update()` to `spawnAsteroid()` and put the "asteroid" prefab into the the script's "asteroid" slot in the "Asteroids" object **Inspector**.
    
    Try running the code now, it should create asteroids much slower.
   
4. If you create too many objects, your computer wont be able to keep track of them all. So when you create an asteroid you need to make sure it is destroyed. Lets use the **Destory()** function in the "DestoryAsteroids" script:

 Attach the "DestroyAsteroids" to the Asteroid prefab. Add `Destroy(gameObject, 10f);` to the `Start()` function.
 
 **gameObject** is the object the script is attached to. 10f destroys the asteroid after ten seconds.
 
5. Lets make your asteroids move! You'll use the "MoveAsteroids" script. Add this above `Start ()`:
  
  ```csharp
  public Rigidbody rb;
  public float asteroidSpeed;
  ```
  
You changed the **Rigidbody**'s **velocity** (the speed) property. `-(transform.up)` is the direction to move. 
  
  
  

    
4. Lets make it more fun by creating them at different locations every spawn. You can make a function that returns a random position to do this!
  
    ```csharp
    Vector3 randomSpawn()
    {
        float xPos = Random.Range(.5f, 9.5f);
        xPos = xPos / 10f;
        Vector3 spawnPosition = Camera.main.ViewportToWorldPoint(new Vector3(xPos, 1.1f, 15f));
        return spawnPosition;
    }
    ```
    Putting **Vector3** instead of **void** in front of a function declaration means that the function will return a **Vector3** object. **Random.Range(.05f, .95f)** returns a random number between the two numbers given in the **parameters** (a parameter is anything in the parenthesis following a function). That number is then divided by 10 so that we get a number between 1 and 0, or the camera's viewport dimensions. You then create a **Vector3** to return called `spawnPosition`. and set the `spawnPosition` to (our randomly generated x position, a y position that is off the screen, the z position that is level with your player object).
    
   Remove these lines:
    
    ```csharp
    spawnPosition.x = 0;
    spawnPosition.y = 0;
    spawnPosition.z = 0;
    ```
    
    Finally, change `Vector3 spawnPosition;` to ` Vector3 spawnPosition = randomSpawn();`. 