# vtp-HausdorffDistance-metric
 
### Motivation :grinning:

Currently, calculating Hausdorff Distance for two pointsets in vtp format is possible by using the [vtkHausdorffDistancePointSetFilter](https://vtk.org/doc/nightly/html/classvtkHausdorffDistancePointSetFilter.html) of vtk library.

However, the current implementation of the filter in vtk only return the bidirectional max hausdorff distance of the two models given.
For further models comparison and evaluation, more performance metrics are needed.

In addition, according to this [post](https://discourse.itk.org/t/computing-95-hausdorff-distance/3832), it seems that there is also no direct usable filter in itk for accessing the calculated distance sets between 2 pointsets.

### The work

The explanation of the current vtk algorithm of hausdorff distance filter is in this [online journal](https://www.vtkjournal.org/browse/publication/839).
The source code of the vtkHausdorffDistancePointSetFilter is in C++.
In this project, the first step was that I referred to the source code of the filter in C++ and implement it in Python.
Then, the python function of the filter was modified to export all the distance sets between the two given pointsets in bidirectional.
Finally, there is a script calculating the min, max, mean, 95 percentile of the given distance sets.
The distance sets are also mapped to the pointsets data as vtp files output for further investigation. (Visualization via python script or Paraview)

The 2 modes of the calculation in the original filter (`PointToPoint` and `PointToCell` ) are also included in this implementation. It is easily configurable by switching the associated parameter in the notebook.

### Validation
A jupyter notebook called `VTP_Phantom_Creation_Script` has been created for testing the new calculation. The 6 vtp files for testing are also included in this repo.

### Reminder
For comparing two 3D model points data, max hausdorff distance should not be the only evaluation metric since it often reflects the local maxima of the 2 pointsets but not the overall performance. I would suggest that 95 percentile and the mean are always good to have. And even "distance" is a scalar unit, in 3D, the directional distance between points are often informative in numerous situations like points missing and point-cell displacements. It is always good to consider these results.
