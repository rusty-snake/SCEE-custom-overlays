# SCEE Custom Overlays

ToC

- Smoothness
- Sidewalk surface
- Highway
- Suspicious highway
- Highway nodes
- Crossing
- Tracktype
- access
- Suspicious access
- Traffic sign
- Barrier
- Traffic calming
- Maxspeed
- Lanes
- All nodes
- Landuse
- Leisure
- Name
- Roof shape
- Levels

## Smoothness

> See, review, edit and maintain road `smoothness`.
> - `highway`s that are `service=driveway`, `service=slipway`, `access=private` or `access=no` are not selected unless they have an existing `smoothness` tag.
> - Dash-filter is used for QA checks on the `surface`.
> - Remember `cycleway:surface` and `footway:surface` tags on `segregated=yes` paths.
>
> We really need a full-featured overlay for this. Hopefully we get it soon. (streetcomplete/StreetComplete#5486)

### Filtering details

```
highway
and service !~ driveway|slipway
and access !~ private|no
or smoothness
```

- [ ] nodes
- [x] ways
- [ ] relations

### Coloring details

```
!smoothness
```

- Highlight missing data: Yes

```
!surface
or (surface ~ unpaved|ground)
or (smoothness = excellent and surface !~ asphalt|concrete|concrete:plates|sett|paving_stones)
or (smoothness = good and surface ~ unpaved|rock|pebblestone|ground|dirt|earth|grass|grass_paver|mud|sand|woodchips|snow|ice)
or (smoothness = intermediate and surface ~ unpaved|rock|ground|dirt|earth|mud|sand|woodchips|snow|ice)
```

## Sidewalk surface

### Filtering details

```
sidewalk:both = yes
or sidewalk:left = yes
or sidewalk:right = yes
or sidewalk ~ both|left|right
```

- [ ] nodes
- [x] ways
- [ ] relations

### Coloring details

```
sidewalk(:both|:left|:right)?:surface
```

- Highlight missing data: Yes

```

```

## Highway

> See, review, edit and maintain the `highway` type of lines.
> - Dash-filter is used to show `oneway`.

### Filtering details

```
highway
```

- [ ] nodes
- [x] ways
- [ ] relations

### Coloring details

```
highway|service|footway
```

- Highlight missing data: No

```
oneway and oneway != no
```

## Suspicious highway

### Filtering details

```
highway = footway
and bicyle = designated
```

- [ ] nodes
- [x] ways
- [ ] relations

### Coloring details

```

```

- Highlight missing data: Yes

```

```

## Highway nodes

> See, review, edit and maintain the `highway` nodes like crossings and other highway related nodes.
> - `bus_stop`s are not selected.

### Filtering details

```
highway
and highway !~ bus_stop|street_lamp
or noexit = yes
or traffic_calming
```

- [x] nodes
- [ ] ways
- [ ] relations

### Coloring details

```
highway|crossing.*|noexit
```

- Highlight missing data: No

```

```

## Crossing

### Filtering details

```
~highway|cycleway|footway ~ crossing
```

- [x] nodes
- [x] ways
- [x] relations

### Coloring details

```
crossing.*
```

- Highlight missing data: Yes

```

```

## Tracktype

> See, review, edit and maintain the `tracktype` of tracks.
> - All `highway=track` are selected.
> - Dash-filter is used for QA checks on the `surface`.


### Filtering details

```
highway=track
```

- [ ] nodes
- [x] ways
- [ ] relations

### Coloring details

```
!tracktype
```

- Highlight missing data: Yes

```
!surface
or tracktype and surface
and (
    (tracktype=grade1 and surface !~ asphalt|concrete|concrete:plates|sett|paving_stones)
    or (tracktype=grade2 and surface !~ compacted|fine_gravel|gravel|shells|pebblestone)
    or (tracktype=grade3 and surface ~ unpaved|ground)
    or (tracktype=grade5 and surface !~ unpaved|fine_gravel|gravel|shells|rock|pebblestone|ground|dirt|earth|grass|mud|sand|woodchips|snow|ice|salt)
    or (surface ~ asphalt|concrete|concrete:plates|sett|paving_stones and tracktype != grade1)
    or (surface ~ ground|dirt|earth|mud|sand and tracktype != grade5)
)
```

## access

### Filtering details

```
(highway and highway !~ bus_stop|street_lamp|give_way)
or barrier ~ block|bollard|coupure|cycle_barrier|entrance|gate|lift_gate|sliding_gate|swing_gate|chain
```

- [x] nodes
- [x] ways
- [x] relations

### Coloring details

```
(oneway:)?(access|foot|dog|ski|inline_skates|horse|portage|vehicle|bicycle|electric_bicycle|mtb|kick_scooter|wheelchair|carriage|cycle_rickshaw|hand_cart|trailer|caravan|motor_vehicle|motorcycle|moped|speed_pedelec|mofa|small_electric_vehicle|motorcar|motorhome|tourist_bus|coach|goods|hgv|hgv_articulated|bdouble|agricultural|auto_rickshaw|nev|golf_cart|microcar|atv|ohv|snowmobile|psv|bus|taxi|minibus|share_taxi|hov|carpool|car_sharing|emergency|hazmat|hazmat:water|school_bus|disabled)?(:forward|:backward)?(:conditional)?
```

- Highlight missing data: No

```

```

## Suspicious access

### Filtering details

```
(access and access != private and !amenity and !leisure)
or agricultural = yes
or bicycle = permissive
```

- [x] nodes
- [x] ways
- [x] relations

### Coloring details

```

```

- Highlight missing data: Yes

```

```

## Traffic sign

### Filtering details

```
traffic_sign
or (highway and highway !~ crossing|traffic_signals|bus_stop)
```

- [x] nodes
- [x] ways
- [ ] relations

### Coloring details

```
!traffic_sign
```

- Highlight missing data: No

```

```

## Barrier

### Filtering details

```
barrier ~ block|bollard|coupure|cycle_barrier|entrance|gate|lift_gate|sliding_gate|swing_gate|chain
```

- [x] nodes
- [x] ways
- [ ] relations

### Coloring details

```
barrier|bollard|cycle_barrier|locked|.*_gate.*
```

- Highlight missing data: No

```

```

## Traffic calming

### Filtering details

```
traffic_calming
```

- [x] nodes
- [ ] ways
- [ ] relations

### Coloring details

```
traffic_calming
```

- Highlight missing data: Yes

```

```

## Maxspeed

### Filtering details

```
highway ~ motorway|trunk|primary|secondary|tertiary|unclassified|residential|motorway_link|trunk_link|primary_link|secondary_link|tertiary_link|service|track|bus_guideway|escape|raceway|road|busway
and (service !~ driveway|parking_aisle or ~maxspeed.*)
and (access !~ private|no or ~maxspeed.*)
or highway and ~maxspeed.*
```

- [ ] nodes
- [x] ways
- [ ] relations

### Coloring details

```
(source:|zone:)?maxspeed.*
```

- Highlight missing data: Yes

```

```

## Lanes

### Filtering details

```
highway ~ motorway|trunk|primary|secondary|tertiary|unclassified|residential|motorway_link|trunk_link|primary_link|secondary_link|tertiary_link|living_street|service|pedestrian|track|bus_guideway|escape|raceway|road|busway
```

- [ ] nodes
- [x] ways
- [ ] relations

### Coloring details

```
lane_markings|(.*:)?lanes(:forward|:backward)?
```

- Highlight missing data: No

```

```

## All nodes

### Filtering details

```
!zögelfrex
```

<sup>If you need to show zögelfrexes, you can use `!tardis` as filter. Showing zögelfrexes and tardises at the same time isn't allowed.</sup>

- [x] nodes
- [ ] ways
- [ ] relations

### Coloring details

```
.*
```

- Highlight missing data: Yes

```

```

## Landuse

### Filtering details

```
(landuse and landuse !~ residential)
or natural
```

- [ ] nodes
- [x] ways
- [x] relations

### Coloring details

```
landuse|natural
```

- Highlight missing data: No

```

```

## Leisure

### Filtering details

```
leisure
```

- [x] nodes
- [x] ways
- [x] relations

### Coloring details

```
leisure
```

- Highlight missing data: No

```

```


## Name

> Everything with a `name` tag.

### Filtering details

```
name
```

- [x] nodes
- [x] ways
- [x] relations

### Coloring details

```
name
```

- Highlight missing data: Yes

```

```

## Roof shape

### Filtering details

```
building
```

- [ ] nodes
- [x] ways
- [x] relations

### Coloring details

```
roof:shape
```

- Highlight missing data: Yes

```

```


## Levels

### Filtering details

```
building
```

- [ ] nodes
- [x] ways
- [x] relations

### Coloring details

```
.*:levels
```

- Highlight missing data: Yes

```

```
