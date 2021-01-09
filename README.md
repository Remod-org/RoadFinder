# RoadFinder
Show and list Rust roads, and use road points programmatically

### Commands
  - /road (Requires roadfinder.use)
    - /road list - List all roads by name, and set temporary markers
	- /road show ROADNAME - Set temporary markers for named road
	- /road {start} ROADNAME - Teleport to the start of the named road in 5 seconds (start is optional)
	- /road end ROADNAME - Teleport to the end of the named road

Ex:
    /road end Road 12 - to teleport to the start of Road 12
	/road start Road 10 - 0
	/road Road 11 - to teleport to the start of Road 11

### Permissions
  - roadfinder.use - Allow use of the road command

### For Developers

```cs
List<string> GetRoadNames();
```

    Returns a List of string values containing road names.

```cs
Dictionary<string, Road> GetRoads();
```

    Returns the entire road list in a Dictionary.  This requires a local version of the following class:

```cs
public class Road
{
    public List<Vector3> points = new List<Vector3>();
    public float width;
    public float offset;
    public int topo;
}
```

```cs
Road GetRoad(string name);
```

    Returns a single Road object for the named road.  Requires class show above.

```cs
List<Vector3> GetRoadPoints(string name);
```

    Returns a list of vectors for the entire run of the road.  The count will vary based on road length.

