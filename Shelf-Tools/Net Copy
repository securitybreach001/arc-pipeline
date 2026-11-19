import os

dir = "//arcanaserver2.arcanastudios.local/ArcanaData2/Artist_Shared/For_Jesus/NETCOPY"
selection = hou.selectedNodes()
codelist = [n.asCode(save_outgoing_wires=True) for n in selection]
#codelist = [n.asCode(False,True) for n in selection]
code = "\n".join(codelist)
print code
    

if(selection != None):
    file = open(dir + "/net_copied.py","w")
    file.write(code)
    file.close()

