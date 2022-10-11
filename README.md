READ ME
Author: Kavi Rangan
Description: I made these scripts to analyze kinesin and mini-dimer (dynein) kymograph images.

Step 1: Use Ilastik to binarize your kymographs. 

Kymographs are assumed to be in the following format: distance on the x-axis and time on the y-axis. You will need to first binarize your kymographs using a pixel classification software. I used Ilastik (https://www.ilastik.org). You can train Ilastik on your own kymographs to get it to classify the pixels appropriately for your signal to noise. For the scripts that I wrote, it is better to err on the side of more noise with continuous tracks, versus less noise and broken up tracks. This is because noise can be filtered out, but broken tracks will be analyzed as separate events.  Your pixel classified kymograph images are assumed to be .jpg, and you should put all the pixel classified kymograph images you want to have analyzed together in a single folder.  

Step 2: Run either kinesin_autotrack (for kinesin analysis) or minidimer_autotrack (for dynein mini-dimer analysis)

These scripts will analyze all the .jpg files in the current directory, and output a .fig file for each .jpg file that shows the skeletonized tracks for you to review, as well as a .mat file that has the analyzed motility parameters for that set of .jpg files. 

**autotrack_images**
Both the kinesin_autotrack and minidimer_autotrack scripts call the script autotrack_images (autotrackkymos6) to convert each pixel classified kymograph image to a series of individual skeletonized tracks that are then analyzed for motility parameters. 
autotrack_images will binarize and skeletonize the pixel classified kymograph image, and remove noise (by removing any tracks 4 pixels or less). To separate crossed tracks, this script will find and erase branchpoints, then stitch the tracks back together based on local slope. It will run iteratively until everything is stitched back together.

**kinesin_autotrack**
This script will analyze kinesin kymographs.
Line references for common parameters you may want to change for your purposes:
-	Framerate on line 48 (currently set as 0.2 sec per y-pixel in the kymograph)
-	Pixelsize on line 49 (currently set as 157 nanometers per x-pixel in the kymograph)
-	Parameters of the findchangepts function on line 123 (currently set as MinDistance = 10; MinThreshold = 10)
-	“Basic plots and Analysis” has a description of the various calculations I performed and you should modify this to suit your preferred thresholds etc.

**minidimer_autotrack**
This script will analyze dynein minidimer kymographs. 
Line references for common parameters you may want to change for your purposes:
-	Framerate on line 47 (currently set as 0.5 sec per y-pixel in the kymograph)
-	Pixelsize on line 48 (currently set as 157 nanometers per x-pixel in the kymograph)
-	Parameters of the findchangepts function on line 123 (currently set as MinDistance = 20; MinThreshold = 10)
-	“Basic plots and Analysis” has a description of the various calculations I performed and you should modify this to suit your preferred thresholds etc.

