<h1 align="center">Manual-BedMesh</h1>
<h3 align="center">A manual bed mesh generation tutorial by VintageGriffin</h3>
<h2 align="center">Why?</h2> 

<p align="center">Gremlins.
  
You've tried everything and your first layer still sucks anywhere but smack in the middle of your bed. 
Plenty of reasons for that: twisted, bent, overtightened X rails or aluminum extrusion, one of Y rails sitting lower than the other to name a few. Also I've been asked this question, so here's a guide. This guide assumes you have a physical Z endstop.</p>

  

<h2 align="center">How?</h2>

<p align="center">Manual labor and wasted plastic. 

Create a blank mesh and load it. Then repeatedly print a full plate of 20x20x0.2 single layer high cubes at mesh point locations, inspecting the level of squish on each cube, deciding whether it needs to be higher or lower, adjusting the corresponding mesh value and doing it again until all cubes come out having that gucci first layer squish we all crave.</p>

  

<h2 align="center">Preparations</h2>

<p align="center">Take the text contents of one of the text files attached below, that contain a blank bed mesh profile for the appropriate bed size - and add them at the bottom of printer.cfg. 
  
  [mesh_250.txt](https://github.com/laserbeak/Manual-BedMesh/files/7796613/mesh_250.txt)
  
  [mesh_350.txt](https://github.com/laserbeak/Manual-BedMesh/files/7796614/mesh_350.txt)

Make sure your printer is going to load this mesh for the calibration prints you'll be doing next. How to do this depends on your printer and slicer configuration, and is not covered here.

Restart klipper to apply all of the config changes you've done up to this point.</p>

<h4 align="center">Open PrusaSlicer or SuperSlicer.</h4>
<p align="center">Temporarily remove your bed texture (if you're using any) so that you can see the coordinate grid. This will make aligning and verifying alignment of test cubes easier.
Right click on bed, add shape, choose Box.
Select it, and in the bottom right corner of slicer window specify the size: 20x20x0.2 (or whatever your layer height is). You may have to click on the lock icon to the left of "Size" so it would allow you to enter all sizes separately without autoscaling.
Right click on your cube, select "Set number of instances" and enter 36 for a 250 and 300 bed sizes, and 49 for a 350 size.
Right click on the Arrange icon at the top and set the slider as close as you can to 30mm for a 300 and 350 sized beds, and 20mm for a 250 bed. This should arrange the cubes in such a way that the center of the bottom left cube starts at 25,25 with the spacing between the centers of adjecent cubes being 40mm for 250 bed, and 50mm for 300 and 350 bed sizes.
Save that as a project so you wouldn't have to repeat the process again.</p>

<h2 align="center">The Loop</h2>
<p align="center">You may want to use an old or already damaged sheet just in case your Z offset is not quite right.

Slice the test model and feed it to your printer. Double check that your (currently) blank mesh is actually loaded during a print.
  
Bring the sheet with the finished print to your computer and under a light source (see attached image).
Inspect printed cubes individually. See if any of them need more or less the amount of squish they currently have (see attached image):
* layer lines should be properly fused and not easy to separate from one another
* drag the tip of your finger over each cube. should feel relatively smooth, with no protruding ridges

Edit the mesh points for cubes that need adjustements. Increase their current mesh value to move nozzle higher (less squish) or decrease it to move nozzle lower (more squish). The value can go into the negatives if needs to (it's relative to the Z endstop position).

Mesh point values are in mm. Start with coarse (multiples of) 0.1mm adjustments, lower them down to 0.05mm, and ultimately to 0.01 as you narrow down your perfect layer height. Keep in mind that the change in value of a mesh point will slightly affect adjacent points. The mesh adjustment for values in between points is interpolated. The only way to really know whether your changes made things better is to print the test again and see.

!DONT FORGET! to put your plate back in the printer before restarting the test print. Don't ask me how I know.

You will need a mesh like this for every significantly different chamber temperature you would be printing at: cold chambers with PLA, hot chambers with ABS. PETG might be fine with the ABS mesh. Testing is the only way to know for sure. This is because a "bed" mesh is a reflection of not only the shape of your bed but also the Z travel of your kinematics and the uneven expansion of all the parts involved; each of which can shift and bend in mysterious ways. Meshing can compensate for most of that.</p>
![full_plate_squish](https://user-images.githubusercontent.com/3384800/147832187-9e729a7a-97ff-4d93-bc67-e22b6ece4dce.png)

![squish_comparison](https://user-images.githubusercontent.com/3384800/147832196-00f91405-1ed8-4b91-ab7e-9c25670607e4.png)
