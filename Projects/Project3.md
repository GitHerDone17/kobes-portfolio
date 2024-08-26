# USF Master Parts Sheet Builder
<br> 

### Overview 
I developed a tool capable of helping utility service engineers build a master parts sheet for the construction of new power lines. The tool follows the Utility Standards Forum (USF), which is a guide on constructing power line assemblies to the proper standard. It conforms with the standards involved in constructing a 28kV line.  
<br>
<br>

### How it works:
Once the tool is launched, there is an 'input' area which is where the end user controls and builds the list. Once a design is created and the standards have been identified, the user can select the necessary standard from the respective dropdown, as well as the quantity of this standard which is required. Once these dropdown options are selected, the user can then hit 'add' which will add the standard to the list, along with the part numbers and quantities required to construct the given standard.

Upon adding all of the desired standards to the material list, the user can then click 'generate pdf' to export the list and have it saved as a pdf file. The 'clear all' button will clear the lists and provide a clean slate for building a new parts list. 

The standards are stored as key/value pairs in a VBA dictionnary. Likewise, all of the button functionality and background work is handled through VBA modules. 
<br> <br> 
[![Download](https://img.shields.io/badge/Download-Excel%20File-blue)](kobes-portfolio/Files/USF_Master_List_Builder.xlsm)

