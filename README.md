# RoadFinder
Show and list Rust roads, rivers, and rails, and use their points programmatically

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
	/road 11 - to teleport to the start of Road 11

The above commands are duplicated for rivers and rails.  Replace road with river or rail, etc.

Note that as of version 1.0.5, you can use just the road number for the target road instead of, e.g. "Road X".

### Permissions
  - roadfinder.use - Allow use of the road command

### Configuration

```json
{
  "Options": {
    "ShowAllTextTime": 30.0,
    "ShowOneTextTime": 60.0,
    "ShowOneAllPoints": true
  },
  "Version": {
    "Major": 1,
    "Minor": 0,
    "Patch": 6
  }
}
```

  - `ShowAllTextTime` -- How long to display start and end points as debug text (at road points)
  - `ShowOneTextTime` -- How long to display start, end and road points for a single road via /road show
  - `ShowOneAllPoints` -- For /road show, display all road points (vs. start and end)

### For Developers
    The following can be used for example as follows:

```cs
    [PluginReference]
    private readonly Plugin RoadFinder;

    Dictionary<string, Road> roads = RoadFinder?.Call("GetRoads");
```

#### Hooks:

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

The above are duplicated for rivers and rails, e.g. GetRiverNames, GetRailNames, etc.

