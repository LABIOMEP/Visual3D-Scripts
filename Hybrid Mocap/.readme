# Hybrid Motion Capture

This software enables the merge of marker trajectories captured with Qualisys at the same time of a markerless data collection using Theia3D software.

## Requirements
A Qualisys Motion Capture system using marker-based (e.g. Oqus) and markerless (e.g. Miqus) cameras. These cameras may be used to collect a given movement using three possibilities:

1. **Hybrid Camera System:** both the marker and markerless cameras are connected to the same computer, and collecting to the same session.
2. **Twin System:** each camera system is collected with a dedicated computer, and the results merged through the Twin System feature of Qualisys.
3. **Synchronized computers:** each camera system is collected with a dedicated computer, but resulting in separated (not merged) files, that are synchronized by a means of sync cable or unit.

In all these cases it is advised that the marker frequency is a multiple of the markerless (video) frequency. This is required so that a resample can be performed to the markers in order to match the frames of the markerless recording.

This tutorial will be focused on presenting the procedure for an (1) Hybrid Camera System, and by using PAF for automation. All the described procedures can be easily reproduced (with the necessary adaptations) for each other camera system option, and for the lack of PAF.

## How does it work
Qualisys PAF manages the process of exporting data to Theia, and directing the resulting kinematics, kinetics and analog data to Visual3D, avoiding the need of a human operator. This is a great time saver, but leaves the trajectories out. This is understandable, since they were not expected in a markerless motion capture.
To add the markers we have two problems:
1. The different sampling frequencies: Usually marker motion capture requires higher (>100 Hz) frequencies than markerless (QTM: 85Hz@fullHD).
2. The fact that Visual3D ASCII import is dependent on the "file owner and path": When creating a CMZ, the C3D filename will include the original path of creation. This means that processing data on other computer may cause some issues, even if both files are related. Example: an hybrid motion capture was performed in PC1. After proessing, the markerless file Trial1.c3d was obtained, and saved at C:\DataCollection\Trial1.c3d. A Visual3D workspace was created and this trial loaded. Then, the workspace was moved to PC2, where the same hybrid C3D file containing the markers was exported from QTM to E:\DataExport\Trial1_markers.c3d. Although both files originated from the same data collection, the original path saves by Visual3D as "owner" is different.
This means that in order to include the markers into a file in VIsual3D we need to perform two operations: 1) resampling the marker frequency, and 2) making sure the markers are associated to the correct "owner".

##  Example Files
1. Open the Gait.cmz. The workspace contains Gait1.c3d, obtained from Theia3D
2. Go to File>Open and select the file Gait 1_markers.c3d
3. Go to Pipeline>Open>MergeHybrid
4. Done!





*Figure 1: Schematic representation of the steps performed to import a marker C3D into a markerless C3D in Visual3D.

## How to 
In Qualisys:
- Create a project for a markerless motion capture;
- Calibrate the system as usual;
- Place markers on the desired object, but not on the participant;
- Collect data;
- Identifiy markers;
- Export C3D or press Process button to send that to Theia3D.

In Theia3D:
- If using PAF, the output of Theia3D will be stored in a CMZ file, and you can jump right to the next step.
- If not using PAF, you'll have to collect the filtered C3D files of Theia with the participant's motion.

In Visual3D
- Open the CMZ containing the markerless data
- Load into the same CMZ the C3D files containing the markers' trajectories
- Run the pipeline "HybridMerge"

After this step you'll have the markers' trajectories associated to the corresponding markerless file.



