# SCEE Custom Overlays

 A collection of custom overlays for SCEE.

ToC

- Smoothness
- Tracktype
- Sidewalk surface
- Sidewalk
- Separate cylceway
- Highway
- Suspicious highway
- Highway nodes
- Crossing
- access
- Suspicious access
- Traffic sign
- Barrier
- Traffic calming
- Maxspeed
- Suspicious Maxspeed
- Lanes
- All nodes
- Landuse
- Leisure
- Name
- Roof shape
- Levels

## Smoothness

See, review, edit and maintain road `smoothness`.
- `highway`s that are `service=driveway`, `service=slipway`, `access=private` or `access=no` are not selected unless they have an existing `smoothness` tag.
- Dash-filter is used for QA checks on the `surface`.
- Keep in mind that there are other surface tags such as `cycleway:surface` and `footway:surface` that are not evaluated by this overlay.
- Tip: Create a "Smoothness" preset for use with this overlay.
- Smoothness overlay request: streetcomplete/StreetComplete#5486

<details><summary>Expand</summary>

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

</details>

## Tracktype

See, review, edit and maintain the `tracktype` of tracks.
- All `highway=track` are selected.
- Dash-filter is used for QA checks on the `surface`.

<details><summary>Expand</summary>

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

</details>


## Sidewalk surface

See, review, edit and maintain the `surface` of sidewalks tagged on streets.

<details><summary>Expand</summary>

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

</details>

## Sidewalk

See and review sidewalks.
- In contrast to the StreetComplete Sidewalk overlay, `separate`d sidewalks are shown.
- Dash-filter is used to show deprecated tags.

<details><summary>Expand</summary>

### Filtering details

```
sidewalk
or sidewalk:both
or sidewalk:left
or sidewalk:right
or (highway ~ path|cycleway|footway and foot != no)
```

- [ ] nodes
- [x] ways
- [ ] relations

### Coloring details

```
sidewalk(:(both|left|right))?
```

- Highlight missing data: Yes

```
sidewalk = none
```

</details>

## Separate cycleways

See and review `cycleway=separate` on streets.
- In contrast to the StreetComplete cylceway overlay, `separate`d cycleways are shown.
- Dash-filter is used to show deprecated tags.

<details><summary>Expand</summary>

### Filtering details

```
~cycleway.* ~ separate
or (highway = path and bicycle = designated)
or (highway = cycleway)
```

- [ ] nodes
- [x] ways
- [ ] relations

### Coloring details

```
cycleway(:(both|left|right))?
```

- Highlight missing data: Yes

```

```

</details>

## Highway

See, review, edit and maintain the `highway` type of ways.
- service type and footway type are colored as well. cycleway type is not colored because the same key is used for tagging cycleways on streets.
- Dash-filter is used to show `oneway`.

<details><summary>Expand</summary>

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

</details>

## Suspicious highway

Find suspicious highways
- footways with `bicycle=designated` may be better tagged as `highway=path`.

<details><summary>Expand</summary>

### Filtering details

```
highway = footway and bicycle = designated
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

</details>

## Highway nodes

See, review, edit and maintain the `highway` nodes like crossings or truning circles and other highway related nodes.
- `bus_stop`s and `street_lamp`s are not selected.
- `noexit=yes` is selected.
- `traffic_calming` is selected.

<details><summary>Expand</summary>

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
highway|crossing.*|noexit|traffic_calming
```

- Highlight missing data: No

```

```

</details>

## Crossing

See, review, edit and maintain `crossing`s.

<details><summary>Expand</summary>

### Filtering details

```
~highway|cycleway|footway ~ crossing
```

- [x] nodes
- [x] ways
- [ ] relations

### Coloring details

```
crossing.*
```

- Highlight missing data: Yes

```

```

</details>

## access

See, review, edit and maintain `access` tags.

<details><summary>Expand</summary>

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
(oneway:)?(access|foot|dog|ski|inline_skates|horse|portage|vehicle|bicycle|electric_bicycle|mtb|kick_scooter|wheelchair|carriage|cycle_rickshaw|hand_cart|trailer|caravan|motor_vehicle|motorcycle|moped|speed_pedelec|mofa|small_electric_vehicle|motorcar|motorhome|tourist_bus|coach|goods|hgv|hgv_articulated|bdouble|agricultural|auto_rickshaw|nev|golf_cart|microcar|atv|ohv|snowmobile|psv|bus|taxi|minibus|share_taxi|hov|carpool|car_sharing|emergency|hazmat|hazmat:water|school_bus|disabled)(:forward|:backward)?(:conditional)?|oneway
```

- Highlight missing data: No

```

```

</details>

## Suspicious access

Find suspicious access tags.
- A plain `access` like `destination` on streets is often a misstagged `motor_vehicle=destination`/`vehicle=destination`.
- `agricultural=yes` is often a misstagged `motor_vehicle=agricultural`.
- `bicycle=permissive` on public footways is not the legal access.

<details><summary>Expand</summary>

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

</details>

## Traffic sign

See, review, edit and maintain `traffic_sign`s.

<details><summary>Expand</summary>

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

</details>

## Barrier

<details><summary>Expand</summary>

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

</details>

## Traffic calming

<details><summary>Expand</summary>

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

</details>

## Maxspeed

See, review, edit and maintain `maxspeed` restrictions.

<details><summary>Expand</summary>

### Filtering details

```
highway ~ motorway|trunk|primary|secondary|tertiary|unclassified|residential|motorway_link|trunk_link|primary_link|secondary_link|tertiary_link|service|track|bus_guideway|escape|raceway|road|busway
and (service !~ driveway|parking_aisle or ~(source:|zone:)?maxspeed.*)
and (access !~ private|no or ~(source:|zone:)?maxspeed.*)
or highway and ~(source:|zone:)?maxspeed.*
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

</details>

## Suspicious maxspeed

Find suspicious `maxspeed` restrictions.
- `living_street`s should not have a maxspeed tagged.
- Maxspeed restrictions on tracks and service roads are often misstagged.

<details><summary>Expand</summary>

### Filtering details

```
highway = living_street and ~(source:|zone:)?maxspeed.*
or highway ~ track|service and ~(source:|zone:)?maxspeed.*
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

</details>

## Lanes

<details><summary>Expand</summary>

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

</details>

## All nodes

Show everythingy, very slow.

<details><summary>Expand</summary>

### Filtering details

```
!zögelfrex
```

<sup>If you need to show zögelfrexes, you can use `!tardis` as filter. Showing zögelfrexes and tardises at the same time isn't allowed.</sup>

- [x] nodes
- [x] ways
- [x] relations

### Coloring details

```
.*
```

- Highlight missing data: Yes

```

```

</details>

## Landuse

See and review `landuse` during surveys. Geometry edits should be done later with Vespucci, iD or JSOM.

<details><summary>Expand</summary>

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

</details>

## Leisure

See and review `leisure` during surveys. Geometry edits should be done later with Vespucci, iD or JSOM.

<details><summary>Expand</summary>

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


</details>

## Name

Everything with a `name` tag.

<details><summary>Expand</summary>

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

</details>

## Roof shape

<details><summary>Expand</summary>

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


</details>

## Levels

<details><summary>Expand</summary>

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

</details>
