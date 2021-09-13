# Houdini-Growth-Infection-Python

This setup allows us to create a Infection geometry on the object level (/obj). Inside the geometry you will see some nodes automaticly created by python code. You can replace your geometry with the Grid which name is "Replace_Your_Geo_Here" so just bring your geo there connect the node after Grid node

There is a Group node which you can set your start point or points from there.

Inside the Solver node you will see another attribwrangle node which you will have the VEX code below and you can play with those three parameters to find the infection style you like



![](https://github.com/s23rcan/Houdini-Growth-Infection-Python/blob/main/Files/vex_infection_data.PNG)

With this VEX code, we will have 3 parameters to control our infection style

Max Distance, Max Poinrs and Infection Speed. 

Max Distance is for how many points we want to jump each frame, for default view try it 3, Max Points is for how many points we want to select around every jumped point and for defauly try it 15. And Infection Speed allows us how fast we want to see infection spreading. Default speed is 1 but to make it slower youo can give 0.1 or 0.01 or less.

# Here is the Python script
You should create a python script from the shell and copy/paste the python code to your houdini python script
and here is code as a link https://github.com/s23rcan/Houdini-Growth-Infection-Python/blob/main/houdini_infection_code.py



![](https://github.com/s23rcan/Houdini-Growth-Infection-Python/blob/main/Files/houdini_script.PNG)
