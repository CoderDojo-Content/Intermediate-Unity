1. The **Graphical User Interface (GUI)** is how your game can display information to the player. You're going to add a score to your game and make the player win or lose.

2. Create an **UI Text** element (**GameObject > UI > Text**) and rename it "Score". In the "Score" **Inspector** there is a text box in the **Text Script** property. Change the text to "Score: 0". This also added an object to your hierarchy called a **Canvas**, this is where all of your GUI elements will be displayed.

3. Play around with the properties in the **Text Script**with the **Inspector**. Make sure you change the color to something that will show up on your background (white works well) and set the **Font Size** to 27.

4. If you check the Game View you will be able to see there the score will be displayed. It's in the center, but you can move it to a better spot. Use the text element's **Rect Transform** in the **Inspector** to move the score into the corner of the screen (use the **x** and **y** values to move it into place).

    ![](/assets/GUIImage.png)

5. Now that you have a place to display the score, you need to update the score. You want to update the score when a laser collides withan asteroid. The code that detects that collision is in the "laserClone" script. However, we need a variable to keep track of the player's score. The score can't be put in the laserClone script because it is destroyed every time the laser it is attached to is destroyed. You will need to use a **static variable**.

   A **static variable** is used to store a variable (with the same value!) across all instances of a class. This means you can use the variable by referencing a class. This can even be referenced from other classes. Without the static keyword you will not be able to access the variable and the value will be different for multiple instances!
   
   Add  to the "Player" script. 
   
   ```csharp
   public static float score;
   ```
   and in the void Start() function
   ```csharp
   score = 0;
   ```
   
6. Now that you have a variable to change, you can update the score in the "OnCollisionEnter()" function in the "laserClone" script.

    ```csharp
    Text displayedScore = GameObject.Find("Score").GetComponent<Text>();
    Player.score = Player.score + 1;
    displayedScore.text = "Score: " + Player.score.ToString();
    ```
    
    **Player.score** is how you access the static variable you made in the Player class. it means from the "Player" class get the "score" variable. **Score.text** is the text that is displayed to the screen for the players score. **ToString()** just converts the score which is a number into a string so it can be displayed. 
    
7. Add a new **UI Text** element to your canvas and call it "winOrLose". Make the text style match your score's text style, then remove all the text from the text box. Change the width of the **Rect Transform** to 200.

8. Now you are going to update the "Player" script so that it updates the "winOrLose" text based on the player losing or winning your game. Since the code will be the same for losing and winning you can create a function so that you don't have duplicate code. Put this function in your "Player" script.

    ```csharp
    void endGame(string text)
    {
        Text endgameText = GameObject.Find("endgameText").GetComponent<Text>();
        endgameText.text = text;
        Time.timeScale = 0;
    }
    ```
    This function requires a parameter or the variable declaration in the parenthesis after the function. This way you can display any text when the function is called. **Time.timeScale** is the speed the game is running at... setting it to 0 stops time in the game.
    
9. The last step to have your player win or lose is calling the function you just added. When the player loses is when they collide with an asteroid, so you should call the "endGame()" function in the **OnCollisionEnter()** function.

    ```csharp
    endgame("GAME OVER");
    ``` 
 
 To make the player win, we can add an if statement in the **Update()** function that checks if the score is equal a number. When the player reaches that number they will win! Add this if statement.

    ```csharp
    if (score = 10)
    {
        endgame("You Win!");
    }
    ```
    Change 10 to whatever number you want the player to get to so that they win.
    
    Your player can now win and lose, and they will get a message when they do!
    
    