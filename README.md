# Houdini-Growth-Infection-Python





obj = hou.node("/obj")
geoNode = obj.createNode("geo", "Growth_Tool")
geoNode.setColor(hou.Color(0.25 , 0.25 ,0.5))


#Nodes are here
gridNode = geoNode.createNode('grid', 'Replace_Your_Geo_Here')
uvNode = geoNode.createNode('uvproject', 'UV_Project')
scatterNode = geoNode.createNode('scatter', 'Scatter')
groupNode = geoNode.createNode('group', 'InfectionGroup')
wrangleNode1 = geoNode.createNode('attribwrangle', 'SetInfection')
solverNode = geoNode.createNode('solver', 'Infection_Animation')
solverNode.setColor(hou.Color(0.25, 0.25, 0.5))
wrangleNode2 = geoNode.createNode('attribwrangle', 'Infection_Color')
nullNode1 = geoNode.createNode('null', 'Out_Infection')
nullNode1.setColor(hou.Color(0.25, 0.25, 0.5))
wrangleNode3 = geoNode.createNode('attribwrangle' , 'Infection_Code')


#Nodes Layout Here
uvNode.setInput(0, gridNode, 0)
scatterNode.setInput(0, uvNode, 0)
groupNode.setInput(0, scatterNode, 0)
wrangleNode1.setInput(0, groupNode, 0)
solverNode.setInput(0, wrangleNode1, 0)
wrangleNode2.setInput(0, solverNode, 0)
nullNode1.setInput(0, wrangleNode2, 0)


geoNode.layoutChildren()


#Parameter Settings Here
uvNode.parm("rx").set("-90")
uvNode.parm("sx").set("50")
uvNode.parm("sy").set("50")
uvNode.parm("sz").set("50")

scatterNode.parm("npts").set("10000")

groupNode.parm("entity").set(1)
groupNode.parm("groupbounding").set(True)
groupNode.parm("boundtype").set(1)

wrangleNode1.parm("group").set("InfectionGroup")
wrangleNode1.parm("snippet").set("f@infection = 1;")

wrangleNode2.parm("snippet").set("@Cd = set(f@infection, 0,0);")
wrangleNode3.parm("snippet").set("if(f@infection < 1){\n\nfloat MaxDistance = chf('Max_Distance');\nint MaxPoints = chf('Max_Points');\nint Array[] = pcfind(0, 'P', @P, MaxDistance, MaxPoints);\nfloat growth = 0;\n\nforeach(int ArrayCounter; Array){\n\n     float infectionGrowth = point(0, 'infection', ArrayCounter);\n     growth += infectionGrowth;\n\n}\n\nfloat div = growth/len(Array);\nf@infection += div;\n\n}      ")


#Network Settings

box = geoNode.createNetworkBox()
box.setColor(hou.Color(0.25,0.25,0.25))



box.addNode(gridNode)
box.addNode(uvNode)
box.addNode(scatterNode)
box.addNode(groupNode)
box.addNode(wrangleNode1)
box.addNode(solverNode)
box.addNode(wrangleNode2)
box.addNode(nullNode1)
box.addNode(wrangleNode3)



box.fitAroundContents()
box.setSize([5,5])
box.setComment("Growth infection sim / Check inside the solver for contro")



#DisplayFlags
nullNode1.setDisplayFlag(True)
nullNode1.setRenderFlag(True)




