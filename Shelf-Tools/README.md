All of these are Houdini Shelf Tools. To use one of them you would need to open one of the files using a note pad app or any other code reading app, copy the contents,and then 
in Houdini you would create a new shelf tool and paste the contets in the script window.

## Import Anim:
Looks at the hip file name to establish what sequence and shot is in. Then finds the latest animation publish folder and loads all the animations creating a chain of prep nodes per abc file. 

## Update Variables: 
Executes the code that set $CAM $BAKES $RENDERS for faster user access to production elements.

## Change Suffix: 
This tool will take the suffix form a specific node type and rename all the “Cache” nodes of the same type inside the selected node. This helps avoid name overrides when working with setups that require several copies of the same FX.
    
## Network Copy:
Allows the user to copy nodes for users with access to the same network.
    
## Network Paste:
Allows the user to paste nodes from users with access to the same network in a different computer using houdini.
