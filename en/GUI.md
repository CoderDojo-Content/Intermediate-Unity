1. The graphical User Interface (GUI) is how your game can display information to the player. You're going to add a menu and a score to your game.

2. Create an **UI Text** element (**GameObject > UI > Text**) and rename it "Score". In the "Score" **Inspector** there is a text box in the **Text Script** property. Change the text to "Score: 0".

3. Play around with the properties in the **Text Script**. Make sure you change the color to something that will show up on your background (white works well) and set the **Font Size** to 27.

4. If you check the Game View you will be able to see there the score will be displayed. It's in the center, but you can move it to a better spot. Use the text element's **Rect Transform** in the **Inspector** to move the score into the corner of the screen.
(**_picture_**)

5. Now that you have a place to display the score, you need to update the score. You want to update the score when a laser destroys an asteroid.