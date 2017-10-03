1. Set the **Transform** of the "Main Camera" position to (0, 0, -15) and set the **Transform** of the "Directional Light" position to (0, 0, -15).

2. Create a 3D Object **Quad** and rename it to "Background" and set the **Transform** position to (0, 0, 1).

3. Drag the background image from the "Materials" folder in the **Project Viewer** and drop it on the Background object in the **Hierarchy**. 

4. Set the **Scale** of x and y on you "Background" **Quad** until it covers the entire Game Display. (Make sure it's set to the "Standalone" Aspect Ratio!) Awesome, you have a background!

5. Now lets add something to control! From the "Prefabs" folder drag and drop the "Player" object onto your scene view. Set the **Transform** position to (0, 0, 0)

6. 

7. To control the game with scripts without attaching them to a 3D object, "Empty Objects" can be used. Create an "Empty Object"(**GameObject > CreateEmpty**). Name this "Obstacles". Create another called "Projectiles".

8. Add the obstacle you downloaded at any position in the scene. Change the scale until you are happy with the object. You need to add a rigidbody component to this object and uncheck the **Use Gravity** box in the **Inspector**. Add a **Box Collider** to this obstacle and make the box bigger than the "Obstacle" object.  