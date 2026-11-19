import os
from os import listdir
from os.path import isfile, join

aprompt = hou.ui.displayMessage("How do you wish to import?", buttons=("Manual", "Auto", "Cancel"))

if aprompt == 0: #IF USER SELECTS MANUAL MODE#
    
    root = hou.ui.readInput("Enter Alembic version directory path:")
    root = root[1]
    print "Manual mode selected"
    print root
    
    
   


elif aprompt == 1: #IF USER SELECTS AUTOMATIC MODE#
    
    print "Automatic mode selected"
    ## GET VARIABLES FROM FILENAME ##
    filename = hou.hipFile.name()
    elements = filename.split("_")
    
    seq = elements[-3]
    shot = elements[-2]
    p_root = "//arcanaserver2.arcanastudios.local/ArcanaData2/Arcana/Production/HGM/3d/io/exports/bakes/"+seq+"/"+shot
    
    #print bakepath
    
    dir_version_paths = []
    
    for dir, sub, file in os.walk(p_root):
        dir = dir.replace('\\','/')
        sub = [n for n in sub]
        sub.sort()
        
       ## FIND VERSION FOLDERS AND BUILD FULL PATHS ##
        
        for f in sub:
            comp = dir+"/"+f
            dir_version_paths.append(comp)
    
    ## GET SIZE FUNCTION ##
    def get_size(start_path = '.'):
        total_size = 0
        for dirpath, dirnames, filenames in os.walk(start_path):
            for f in filenames:
                fp = os.path.join(dirpath, f)
                # skip if it is symbolic link
                if not os.path.islink(fp):
                    total_size += os.path.getsize(fp)

        return total_size


   # Find a valid version (in this case if the last version doesn't contain anything, the previous one surely will) #         
    
    latest_versions =  dir_version_paths[-2:]

    if get_size(latest_versions[-1]) > 150:
        root = latest_versions[-1]
    else:
        root = latest_versions[0]
    #print "Root is:" + root +"\n"
        
            
   
#Wipe out Geo_Sort1--------------------------------# 
scaleNode = hou.node('/obj/Hou_Scale')
if aprompt != 2:

    old_geoSort = hou.node('/obj/Geo_Sort1')
    pos = old_geoSort.position()
    old_geoSort.destroy()
    
    obj = hou.node("/obj")
    geoSort = obj.createNode("geo","Geo_Sort1")
    geoSort.setPosition(pos)
    geoSort.setDisplayFlag(False)
    geoSort.setNextInput(scaleNode,0)
    
    
   
        

else:
    hou.ui.displayMessage("Aborted")
    
## Create Naming Function ##
def rename(i):
    
    if "HumanJiahao" in i:
        i = "Jiahao"
    
    if "AtlanteanAesop" in i:
        i = "Aesop"
        
    elif "Hammer" in i:
        i = "Hammer"
        
    elif "MaskAesop" in i:
        i = "AesopsMask"
        
    elif "HumanLi" in i:
        i = "Li"
        
    elif "LisBow" in i:
        i = "Bow"
        
    elif "MaskLis" in i:
        i = "Lis_Mask"
        
    elif "HumanZhu" in i:
        i = "Zhu_A"
        
    elif "HumanZhu" in i:
        i = "Zhu_A"
    
    elif "Zhu1RN" in i:
        i = "Zhu_B"
        
    elif "MaskZhus" in i:
        i = "Zhus_Mask"
        
        
    elif "SET_Sanxingdui1" in i:
        i = "Set"
        
             
    elif "WeaponPokatokBalls1" in i:
        i = "Pokatok_1"
        
    elif "WeaponPokatokBalls2" in i:
        i = "Pokatok_2"
        
    elif "WeaponPokatokBalls3" in i:
        i = "Pokatok_3"    
        
    elif "HumanKunYi" in i:
        i = "Kunyi"  
        
    elif "Statue" in i:
        i = "Statue" 
        
        
    elif "SET" in i:
        i = "Set"
    
    return i
    
def getColor(i):

    if "Aesop" in i:
        c = (0.0,1.0,0.209)
        
    elif "Li" in i:
        c = (0.643,0.161,1)
        
    elif "Jiahao" in i:
        c = (0.0,0.632,0.69)
        
    elif "Charlie" in i:
        c = (0.0,0.632,0.69)
        
    elif "Zuma" in i:
        c = (0.8,0.016,0.016)
        
    elif "PokatokBalls" in i:
        c = (0.8,0.016,0.016)
        
    elif "Zhu" in i:
        c = (1.0,0.725,0)
        
    elif "KunYi" in i:
        c = (0.3,0.3,0.3)
        
    elif "Soldier" in i:
        c = (0.6,0.6,0.6)
        
        
    elif "WeaponCommon" in i:
        c = (0.6,0.6,0.6)
          
    else:
        c = (1,1,1)
        
    return c
    
# List Alembic files inside root directory # ---------------- 
abcfiles = [f for f in listdir(root) if isfile(join(root, f))]

#abcfiles.remove("offsets.json")


 

num_nodes = len(abcfiles)
#print num_nodes
i = 0
for name in abcfiles:

    ## PRIMARY ALEMBIC ##
    
    filepath = root + "/" + name
    readable = rename(name)
    #color = (0,1,0)
    color = getColor(name)
    
 
    
    
    
    pos = hou.Vector2((i*5),0)
    currentNode = geoSort.createNode("alembic",name)    
    currentNode.setPosition(pos)
    currentNode.setDisplayFlag(False)
    currentNode.setColor(hou.Color(color))
    currentNode.parm("fileName").set(filepath)
    
    if "Mask" not in readable:
    
        ## MERGE NODE ##
        mergeNode = geoSort.createNode("merge","merge")
        m_pos = hou.Vector2((i*5),(-2))
        mergeNode.setPosition(m_pos)
        mergeNode.setDisplayFlag(False)
        mergeNode.setNextInput(currentNode,0)
    
        ## IMPORT PREP ##
        iprepNode = geoSort.createNode("arc::importPrep::0.1","importPrep")
        i_pos = hou.Vector2((i*5),(-3))
        iprepNode.setPosition(i_pos)
        iprepNode.setDisplayFlag(False)
        iprepNode.setNextInput(mergeNode,0)  
        
        ## Cache Node ##
        cacheNode = geoSort.createNode("Arc::arcCache::1.8","import_cache_" + readable)
        c_pos = hou.Vector2((i*5),(-4))
        cacheNode.setPosition(c_pos)
        cacheNode.setDisplayFlag(False)
        cacheNode.setNextInput(iprepNode,0)
        
        ## Null Output ##
        outNode = geoSort.createNode("null","OUT_"+readable)
        n_pos = hou.Vector2((i*5),(-5))
        outNode.setPosition(n_pos)
        outNode.setDisplayFlag(True)
        outNode.setRenderFlag(True)
        outNode.setNextInput(cacheNode,0)
       
    
    i += 1
