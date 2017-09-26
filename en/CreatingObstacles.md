1. Create a new C# script in the "Scripts" folder named "Obstacles" and Attach it to the "Obstacles" **GameObject** you created earlier.

2. 

  ```csharp
  public GameObject obstacle;
  public float spawnTime = .5f;
  public float obstacleSpeed = 2f;
   
  // Use this for initialization
  void Start()
  {
    // 0f is when to start invoking repeat
    InvokeRepeating("spawnObstacle", 0f, spawnTime);
  }
   
  void spawnObstacle()
  {
    // Creating clones
    Vector3 spawnPosition;
    spawnPosition.x = 0;
    spawnPosition.y = 0;
    spawnPosition.z = 0;
    GameObject asteroidClone = Instantiate(obstacle, spawnPosition, obstacle.transform.rotation) as GameObject;
    // Move clones
    Rigidbody asteroidCloneRB = asteroidClone.GetComponent<Rigidbody>();
    asteroidCloneRB.velocity = -(transform.up * asteroidSpeed);
    // Make sure clone is destroyed
    Destroy(asteroidClone, 10f);
  }
  ```