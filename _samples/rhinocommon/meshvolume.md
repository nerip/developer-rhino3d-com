---
layout: code-sample
title:  Volume of Meshes 
author: 
categories: ['Other'] 
platforms: ['Cross-Platform']
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB.NET']
keywords: ['volume', 'meshes']
order: 111
description:  
---



```cs
public class MeshVolumeCommand : Command
{
  public override string EnglishName { get { return "csMeshVolume"; } }

  protected override Result RunCommand(RhinoDoc doc, RunMode mode)
  {
    var gm = new GetObject();
    gm.SetCommandPrompt("Select solid meshes for volume calculation");
    gm.GeometryFilter = ObjectType.Mesh;
    gm.GeometryAttributeFilter = GeometryAttributeFilter.ClosedMesh;
    gm.SubObjectSelect = false;
    gm.GroupSelect = true;
    gm.GetMultiple(1, 0);
    if (gm.CommandResult() != Result.Success)
      return gm.CommandResult();

    double volume = 0.0;
    double volume_error = 0.0;
    foreach (var obj_ref in gm.Objects())
    {
      if (obj_ref.Mesh() != null)
      {
        var mass_properties = VolumeMassProperties.Compute(obj_ref.Mesh());
        if (mass_properties != null)
        {
          volume += mass_properties.Volume;
          volume_error += mass_properties.VolumeError;
        }
      }
    }

    RhinoApp.WriteLine("Total volume = {0:f} (+/- {1:f})", volume, volume_error);
    return Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Public Class MeshVolumeCommand
  Inherits Command
  Public Overrides ReadOnly Property EnglishName() As String
    Get
      Return "vbMeshVolume"
    End Get
  End Property

  Protected Overrides Function RunCommand(doc As RhinoDoc, mode As RunMode) As Result
    Dim gm = New GetObject()
    gm.SetCommandPrompt("Select solid meshes for volume calculation")
    gm.GeometryFilter = ObjectType.Mesh
    gm.GeometryAttributeFilter = GeometryAttributeFilter.ClosedMesh
    gm.SubObjectSelect = False
    gm.GroupSelect = True
    gm.GetMultiple(1, 0)
    If gm.CommandResult() <> Result.Success Then
      Return gm.CommandResult()
    End If

    Dim volume As Double = 0.0
    Dim volume_error As Double = 0.0
    For Each obj_ref As ObjRef In gm.Objects()
      If obj_ref.Mesh() IsNot Nothing Then
        Dim mass_properties = VolumeMassProperties.Compute(obj_ref.Mesh())
        If mass_properties IsNot Nothing Then
          volume += mass_properties.Volume
          volume_error += mass_properties.VolumeError
        End If
      End If
    Next

    RhinoApp.WriteLine("Total volume = {0:f} (+/- {1:f})", volume, volume_error)
    Return Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
from Rhino.Input.Custom import *
from Rhino.DocObjects import ObjectType
from Rhino.Geometry import *
from Rhino.Commands import Result

def RunCommand():
  gm = GetObject()
  gm.SetCommandPrompt("Select solid meshes for volume calculation")
  gm.GeometryFilter = ObjectType.Mesh
  gm.GeometryAttributeFilter = GeometryAttributeFilter.ClosedMesh
  gm.SubObjectSelect = False
  gm.GroupSelect = True
  gm.GetMultiple(1, 0)
  if gm.CommandResult() != Result.Success:
    return gm.CommandResult()

  volume = 0.0
  volume_error = 0.0
  for obj_ref in gm.Objects():
    if obj_ref.Mesh() != None:
      mass_properties = VolumeMassProperties.Compute(obj_ref.Mesh())
      if mass_properties != None:
        volume += mass_properties.Volume
        volume_error += mass_properties.VolumeError

  print "Total volume = {0:f} (+/- {1:f})".format(volume, volume_error)
  return Result.Success

if __name__ == "__main__":
  RunCommand()
```
{: #py .tab-pane .fade .in}

