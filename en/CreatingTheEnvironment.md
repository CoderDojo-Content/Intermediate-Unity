1. set the **Transform** the "Main Camera" to (0, 0, -15)

2. Create a 3D Object **Quad** and rename it to "Background"
3. Set the **Transform** of the "Background" Object to (0, 0, 1).

4. Drag the background image you chose earlier from the "Materials" folder in the **Project Viewer** and drop it on the Background object in the **Hierarchy**. 

5. Set the **Scale** of x and y on you "Background" **Quad** until it covers the entire Game Display. (Make sure it's set to the "Standalone" Aspect Ratio!) Awesome, you have a background!

6. Now lets add something to control! Select the 3D object you chose earlier for you player and put it in the scene at position (0, 0, 0).

7. To control the game with scripts without attaching them to a 3D object, "Empty Objects" can be used. Create an "Empty Object"(**GameObject>CreateEmpty**). Name this "Obstacles". Create another called "Projectiles".