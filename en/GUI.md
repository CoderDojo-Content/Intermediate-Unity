1. The graphical User Interface (GUI) is how your game can display information to the player. You're going to add a menu and a score to your game.

2. Create an **UI Text** element (**GameObject > UI > Text**) and rename it "Score". In the "Score" **Inspector** there is a text box in the **Text Script** property. Change the text to "Score: 0".

3. Play around with the properties in the **Text Script**. Make sure you change the color to something that will show up on your background (white works well) and set the **Font Size** to 27.

4. If you check the Game View you will be able to see there the score will be displayed. It's in the center, but you can move it to a better spot. Use the text element's **Rect Transform** in the **Inspector** to move the score into the corner of the screen.
(**_picture_**)

5. Now that you have a place to display the score, you need to update the score. You want to update the score when a laser collides an asteroid. The code that detects that collision is in the "laserClone" script. However, we need a variable to keep track of the player's score. The score can't be put in the laserClone script because it is destroyed every time the laser it is attached to is destroyed. You will need to use the **static variable**.

   A **static variable** is used to store a variable across all instances of a class. This means you can use the variable by referencing a class. This can even be referenced from other classes.
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
    Text Score = GameObject.Find("Text").GetComponent<Text>();
    Player.score = Player.score + 1;
    Score.text = "Score: " + Player.score.ToString();
    ```
    
    **Player.score** is how you access the static variable you made in the Player class. it means from the "Player" class get the "score" variable. **
    
    
    