1. You'll use a few scripts for your asteroids, so to keep organized it's a good idea to make an "Asteroids" folder. Now, you will need 3 new C# scripts: CreateAsteroids, MoveAsteroid, and DestroyAsteroid.

2. Attach the "CreateAsteroids" script to  "CreateAsteroids" and add this code:

  ```csharp
  public GameObject asteroid;
   
  void Update()
  {
    Vector3 createPosition = Vector3.zero;
    Instantiate(asteroid, createPosition, asteroid.transform.rotation)
  }
  ```
  To understand what's happening here you need to know what **instantiate** means. **Instantiating** something is like building something from plans or instructions. If you're baking a cake, the cake is the **instance** and the recipe is the **Instantiate()** function. In the game world, your cake is instead a **GameObject**!

  Drag the Asteroid prefab form the "Prefabs" folder and drop it into the "asteroid" box for your "CreateAsteroids" script in the **Inspector** for your "Asteroids" object. Try running your game.

3. WOAH! That was a lot of asteroids being created!The **Update()** function happens really fast so a lot of asteroids get created. You can control how fast the asteroids are created with the `InvokeRepeating()` function. Add this to your previous code:

    ```csharp
    public float creationTime = 1f;
    
    // Use this for initialization
    void Start()
    {
    // 0f is when to start invoking repeat
    InvokeRepeating("createAsteroid", 0f, creationTime);
    }
    ```
    
    Now change `Update()` to `createAsteroid()` and put the "asteroid" prefab into the the script's "asteroid" slot in the "Asteroids" object **Inspector**.
    
    Try running the code now, it should create asteroids much slower.
   
4. If you create too many objects, your computer wont be able to keep track of them all. So when you create an asteroid you need to make sure it is destroyed. Lets use the **Destory()** function in the "DestoryAsteroids" script:

 Attach the "DestroyAsteroids" to the Asteroid prefab. Add `Destroy(gameObject, 10f);` to the `Start()` function.
 
 **gameObject** is the object the script is attached to. 10f destroys the asteroid after ten seconds.
 
5. Lets make your asteroids move! You'll use the "MoveAsteroids" script. Add this above `Start ()`:
  
  ```csharp
  public Rigidbody rb;
  public float asteroidSpeed;
  ```
  and this into `Start()`:
  `rb.velocity = -(transform.up) * asteroidSpeed`
  
  You changed the **Rigidbody**'s **velocity** (the speed) property. `-(transform.up)` is the direction to move.

  The final step is attaching the asteroid prefab's **Rigidbody** to the "MoveAsteroid" script and set the value of **asteroidSpeed** to 2.
 
  ![](en/assets/unityRBattach.png) 

6. Lets make it more fun by creating asteroids at different. You can make a function that returns a random position to do this! Add this function to the "CreateAsteroids" script:
  
    ```csharp
    Vector3 getRandomPosition()
    {
        float xPos = Random.Range(.05f, .95f);
        Vector3 randomPosition = Camera.main.ViewportToWorldPoint(new Vector3(xPos, 1.1f, 15f));
        return randomPosition;
    }
    ```
    Putting **Vector3** instead of **void** in front of a function declaration means that the function will return a **Vector3** object. 
    
    **Random.Range(.05f, .95f)** returns a random number between the two numbers given in the **parameters** (a parameter is anything in the parenthesis following a function). 
    
  The camera's viewport dimensions are 1 by 1 (the bottom left being (0,0) and the top right being (1,1)). 
  
  You then create a **Vector3** to return called `randomPosition`. and set the `randomPosition` to (our randomly generated x position, a y position that creates the asteroids above the screen, and the z position that is level with your player object).
  
  Finally, change `Vector3 createPosition;` to ` Vector3 createPosition = getRandomPosition();`.
  
7. Try the game out!