# Hybrid Motion Capture

This software enables the post-processing merge of marker trajectories captured with a marker-based motion capture at the same time of a markerless system such as Theia3D.

## Requirements
A Qualisys Motion Capture system using marker-based (e.g. Oqus) and markerless (e.g. Miqus) cameras. These cameras may be used to collect a given movement using three possibilities:

1. **Hybrid Camera System:** both the marker and markerless cameras are connected to the same computer, and collecting to the same session.
2. **Twin System:** each camera system is collected with a dedicated computer, and the results merged through the Twin System feature of Qualisys.
3. **Synchronized computers:** each camera system is collected with a dedicated computer, but resulting in separated (not merged) files, that are synchronized by a means of sync cable or unit.

In all these cases it is advised that the marker frequency is a multiple of the markerless (video) frequency. This is required so that a resample can be performed to the markers in order to match the frames of the markerless recording.

This tutorial will be focused on presenting the procedure for an (1) Hybrid Camera System, and by using PAF for automation. All the described procedures can be easily reproduced (with the necessary adaptations) for each other camera system option, and for the lack of PAF.

*Although this scipt has been created for use within a Qualisys environment, it should be possible to use C3D files from other sources, sine all processing is done in Visual3D*

## How does it work
In order to allow the present of C3D files with the same name (e.g. Trial1.c3d) within the same workspace, Visual3D takes in consideration the file's original path (https://www.c-motion.com/v3dwiki/index.php/File_Names).
If the C3D continaing marker information and the one with the markerless that have the same name and path, this is an easy in Visual3D. It is only necessary to open the marker C3D and export the Targets to an ASCII file. Then, import that ASCII file into the markerless C3D file. As long as both C3D files have the same name and path, that is straightforward.
However, problems arise when files have a different path (despite the same name). In this case it is necessary to change the "file ownership". This is easily done manually by changing the marker-based ASCII file header to that of the markerless C3D fullpath name (including the original path and filename).
Adding to these difficulties, these system usually have different sampling frequencies, requiring a downsampling of the markers to match the markerless.

For a year, our laboratory has made this process somewhat manually. However, large quantities of data and the increasing need of having to collect markers along with markerless motion capture sessions, made us develop the scripts now made available.

## Use and limitations
We tried to create a generic script, that will handle any kind of data and names.
While simple to add markers to dynamic trials, its inclusion on the Visual3D model is a little more complicated. When exporting the model and then merge with markers, the model does not behave as expected. As such, we created to scripts:
- MergeHybrid: allows the merge of markers to markerless in dynamic conditions (does not alter the calibration file).
- MergeHybridStatic: allows the merge of markers to markerless in dynamic conditions. It also creates a new calibration file from 5 frames of a dynamic file.

## Files needed
To run these scrips you'll need:
- A Visual3D workspace with the markerless C3D files already loaded
- A set of C3D files with marker information, corresponding to the files in the V3D workspace. These files should have the same name as the markerless ones.

##  Example Files
We provide two examples for you to practive this method of post-processing merge:
- Golf
- Weighlifting

Each folder has all the files needed to run the script.
A second workspace is presented with the result of the script.

## How to
# HybridMerge
1. Open the Golf.cmz in Visual3D
2. Load and execute the pipeline MergeHybrid.v3d
3. Select the markerless system sampling frequency (this will downsample the markers)
4. Select the marker-based C3D files to merge. You can select all at the same time.
5. Wait for the downsampling
*Note: if Visual3D crashes while downsampling, it means that the imported marker C3D file was missing marker information (is empty).*
6. Save the new Workspace.

# HybridMergeStatic
1. Open the Golf.cmz in Visual3D
2. Load and execute the pipeline MergeHybrid.v3d
3. Select the markerless system sampling frequency (this will downsample the markers)
4. Select the marker-based C3D files to merge. You can select all at the same time.
5. Wait for the downsampling
*Note: if Visual3D crashes while downsampling, it means that the imported marker C3D file was missing marker information (is empty).*
6. Select a file from the workspace to be used as Static Calibration file.
7. Confirm the assignment removel of the old model (just press OK).
8. Go to the Model tab. You may add new rigid bodies based on the markers, or press "Build", as this script did not perform this step.
9. Save the new Workspace.

*Disclaimer: these scrips and files are provided for research and teaching purpose. Their use for comercial purposes is not allowed without prior and written authorization from LABIOMEP board of directors.*



