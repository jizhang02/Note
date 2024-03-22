# Practice on medical imaging processing software
#### Medical Image Analysis Using FIJI software
* open/import a specific file in different formats
* zoom in/out an image: +/- key
* browse a slice: left/right key
* see 3D image in 3 directions
  * stacks->orthogonal views  
  * stacks->reslice '/' key
* compute mean/std value: 'm' key
  * results/analyse->set measurements
  * the whole slice
  * the selected area 
* Image->Lookup Tables, set different show ways
* Analyse->Plot profile, make a plot of selected area
* Image->Stacks->Statistics, statistics of a image
* Image->Show Info, save image info to a file
* Color bar: Analyze > Tools > Calibration Bar
* View 3D imagein 3 directions: Ctrl+Shift+H
* Image > Stacks > Make Montage: show all slices in a table
* Image > Stacks > Images to Stack: make multiple images into a stack
* Image > Stacks > Z Project (Max intensity): make all the max value of slices into one slice
* Image > Stacks > Z Project (Average intensity): make all the average value of slices into one slice
* Image > Stacks > Z Project (Sum slices): make all the slices into one slice
* Process > Enhance Contrast: show pet image more clearly
* Image > Overlay: add another image on the current image
* Export GIF: Image > Stacks > 3D Project, then click File > Save as > GIF

#### Medical Image Analysis Using Slicer software
* generate a gif 
  * Modules-> Utilities->ScreenCapture
  * Output type: video, image series, lightbox image
* show : click left-up coner buttons on three views respectily
* Color bar: Volume > Color Legend. Or right click the image to show the color legent
* Overlay: Left upper coner of show panel > F > B 
* MIP: Lookup tables > PET-Maximum Intensity Projection
* Isodose: In radiotherapy, set threshold value of each line

#### Medical Image Analysis Using ITK-SNAP software
* It is easy to open a CT and PET image in one window or both two windows, the position is the same.
* Adjust the contrast by clicking auto mode.
* Load segmentation masks on the CT images and segmentation organs in 3D mode.
* PaintBrush Mode on masks->Right click, remove label; Left click, add label.
* Polygon Mode -> Draw line on current label -> accept -> move to next slide -> paste last polygon -> drag the line to fine tune.
* LabelEditor -> Hide certain labels in all windows to only show one label.
* LabelEditor -> Actions -> Import/Export Label Descriptions.
* 
