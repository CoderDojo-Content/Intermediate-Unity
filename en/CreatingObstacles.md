1. Create a new C# script in the "Scripts" folder named "Obstacles" and Attach it to the "Obstacles" **GameObject** you created earlier.

2. Create a new folder and name it "Prefabs". Drag your obstacle from the **hierarchy** and drop it in the "Prefabs" folder. Name this prefab "obstacle".

3. Add this code to you "Obstacles" script and drag the obstacle prefab you made and drop it into the "obstacle" box for your "obstacles" script in the **Inspector** for your "Obstacles" object.

  ```csharp
  public GameObject obstacle;
  public float obstacleSpeed = 2f;
   
  void Update()
  {
    // Creating clones
    Vector3 spawnPosition;
    spawnPosition.x = 0;
    spawnPosition.y = 0;
    spawnPosition.z = 0;
    GameObject obstacleClone = Instantiate(obstacle, spawnPosition, obstacle.transform.rotation) as GameObject;
    // Move clones
    Rigidbody obstacleCloneRB = obstacleClone.GetComponent<Rigidbody>();
    obstacleCloneRB.velocity = -(transform.up * obstacleSpeed);
    // Make sure clone is destroyed
    Destroy(obstacleClone, 10f);
  }
  ```
  To understand what's happening here you need to know what **instantiate** means. Instantiating something is creating a copy of a template. The template is the first object you pass into the **Instantiate()** function. In your case it is a **GameObject**! However, when you instantiate an object you must **Destroy()** it or your computer will slow down! The last line of this code destroys the instantiated object after 10 seconds.
  
  To make your obstacles move at a constant velocity you change the **Rigidbody**'s **velocity** component.
  
4. WOAH! That was a lot of obstacles spawning! When you're repeatedly spawning an obstacle, you want to be able to control how fast it spawns. To do that you can us a built in function! Add this to your code:

    ```csharp
    public float spawnTime = 1f;
    
    // Use this for initialization
    void Start()
    {
    // 0f is when to start invoking repeat
    InvokeRepeating("spawnObstacle", 0f, spawnTime);
    }
    ```
    
    Now change `Update()` to `spawnObstacle()`.
    (Change the spawnTime variable so that your obstacles don't hit each other!)
    
5. Now your obstacles spawn at a reasonable speed, but they only spawn in the same location. Lets make it more fun by spawning them at different locations every spawn. You can make a function that returns a position to do this!
  
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
    
    Finally, change `Vector3 spawnPosition;` to ` Vector3 spawnPosition = randomSpawn();`