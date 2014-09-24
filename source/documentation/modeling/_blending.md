###Blending the Junction of Two Vessels

The idea behind blending two faces of a model together is similar to sweeping a clay sphere of a certain radius all along the seam to “fill in the cracks” and make it smoother. In order to blend your model, you will first have to know the names of the faces you will be blending.

At the end of the last exercise, we learned how to view the model. From the “Model” tab, you will notice a list of “Face Ids”. When you highlight these numbers, you will notice the field next to “surf name:” changing. 

You should have two faces whose names start with “wall” followed by the group names. 
For each of these “wall” faces, click on the “Change Color” button and choose a different color for them. This will ensure that the walls you are choosing to blend are what you think they are.

In our case, the two walls we would like to blend are named “wall_aorta_test” and “wall_right_iliac2”. Take note of these names. We have changed the surfaces to be pink and sky blue, respectively:

<figure>
<img  src="documentation/modeling/imgs/solid_modeling/blending/1.jpg" width="100%"> 
</figure>

Now is also a good time to change the names of all the faces to be more descriptive. Change the name of the pink and sky blue surfaces to be “wall_aorta_test” and “wall_right_iliac,” if they do not already have those names. In the figure below, we have changed the color of the face that we will name “inflow_aorta_test” to yellow, “outflow_aorta_test” to green, and “outflow_right_iliac” to blue as shown below. To change the name of each face, click on the corresponding “Face Id”, type in the corresponding name in the “surf name:” field, and click the “Set Value” button. For future reference, the names of the faces are case sensitive so try to be consistent when capitalizing. We recommend that you use only lower case letters in your face names.

<figure>
<img  src="documentation/modeling/imgs/solid_modeling/blending/2.jpg" width="100%"> 
</figure>

Next, navigate to the “Parasolid → Blend Model” tab. Next to “Solid model file:”, browse for the solid model you created and then click “Load”.

In the bottom frame of the “Blend Model” tab, you will find a field with three columns, labeled “face 1”, “face 2”, and radius. Type in the two names of the “wall” faces you would like to blend, and then type in “0.3” for the radius. At least one space must be separating each of these typed fields.

When you are done, click on the “Blend Model” button. Clear the window of your previous model. Navigate back to the “View Model” tab, and next to the “Solid Model Object:” field, select “Blended Solid”. Your blended model should now appear. Zoom in to the bifurcation area. You can highlight the blended surface by putting your mouse over it and typing “p” on the keyboard to turn it yellow:

<figure>
<img  src="documentation/modeling/imgs/solid_modeling/blending/3.jpg" width="100%"> 
</figure>

You’ll see how blending the model created a surface that “smoothed over” the previous seam. What happens when you choose a different radius for blending?  Play around with different values for the radius, clicking on “Blend Model” after you have changed the radius value. Then clear the 3D window and re-display the blended model under the “Model” tab.

Note: If there is a case where the “blending sphere” radius is such that it intersects a wall twice (you have a very tight junction), the two walls will not blend. Try decreasing the radius in these cases.

When you are satisfied with the level of blending you have chosen for your model, navigate back to the “Blend Model” tab, and under the “Blended Solid Model” heading, type in a file name in the “Solid model file”. You should indicate in the file name that this is your blended model, and keep the “.xmt_txt” file extension. Click on the “Save” button to save this model:

<figure>
<img  src="documentation/modeling/imgs/solid_modeling/blending/4.jpg" width="100%"> 
</figure>