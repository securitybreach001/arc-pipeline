import hou
import sys

key = ("Arc","arcCache")

targets = []

selected = hou.selectedNodes()

if len(selected) == 0:
    hou.ui.displayMessage("Select one OBJ node and try again:")
    sys.exit("")

if len(selected) > 1:
    hou.ui.displayMessage("Select only one OBJ node at a time and try again")
    sys.exit("")


#r = selected.


for n in selected:
    
    chi = n.children()
    node = n
    
    
    #node = hou.node(n)
    #print hou.nodeType(n)
    #print type(n)
suffix = node.name().split("_")[-1]



for n in chi:
    #print type(n)
    type = n.type()
    components = type.nameComponents()
    name = n.name()
    
    if components[1:3] == key or name.split("_")[0] == "REF":
        #targets.extend(n.instances())
        newname = name + "_" + suffix
        print newname
        n.setName(newname)
 
hou.ui.displayMessage("Arc Cache nodes renamed successfully")
