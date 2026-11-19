
## GET VERSION FROM FILENAME ##
filename = hou.hipFile.name()
elements = filename.split("_")
extver = elements[-1].split(".")



try: 
    ver = extver[-2]

    ## GET SEQUENCE AND SHOT FROM FILE NAME##

    seq = elements[-3]
    shot = elements[-2]

    ## Check if the file name is correct ##
         
    ##ASSIGN VARIABLES##
    hou.putenv("VER",str(ver))
    hou.putenv("SEQ",str(seq))
    hou.putenv("SHOT",str(shot))
    
    
    hou.hscript('varchange')
    
    camerapath = "//arcanaserver2.arcanastudios.local/ArcanaData2/Arcana/Production/HGM/3d/io/exports/cameras/"+seq+"/"+shot
    bakepath = "//arcanaserver2.arcanastudios.local/ArcanaData2/Arcana/Production/HGM/3d/io/exports/bakes/"+seq+"/"+shot
    renderpath = "//arcanaserver2.arcanastudios.local/ArcanaData2/Arcana/Production/HGM/3d/io/renders/"+seq+"/"+shot+"/FX"
    
    hou.putenv("CAMERAPATH",str(camerapath))
    hou.putenv("BAKEPATH",str(bakepath))
    hou.putenv("RENDERPATH",str(renderpath))
    
    
    hou.hscript('setenv CAM = $CAMERAPATH')
    hou.hscript('setenv BAKES = $BAKEPATH')
    hou.hscript('setenv RENDERS = $RENDERPATH')

    #hou.putenv("CAM",str(camerapath))
    #hou.putenv("BAKES",str(bakepath))
    

except:
    print ""
