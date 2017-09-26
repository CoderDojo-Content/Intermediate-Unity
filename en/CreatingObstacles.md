1. Create a new C# script in the "Scripts" folder named "Obstacles" and Attach it to the "Obstacles" **GameObject** you created earlier.

2. 

  ```csharp
  public GameObject obstacle;
  public float spawnTime = .5f;
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
    obstacleCloneRB.velocity = -(transform.up * asteroidSpeed);
    // Make sure clone is destroyed
    Destroy(obstacleClone, 10f);
  }
  ```
  
  When you're repeatedly spawning an obstacle, you want to be able to control how fast it spawns. 