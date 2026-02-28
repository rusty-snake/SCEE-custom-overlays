# SCEE Custom Overlays for POI

These are overlays for features that can be edited better with [Every Door](https://every-door.app/).

## Traffic sign

See, review, edit and maintain `traffic_sign`s.

<details><summary>Expand</summary>

### Filtering details

```
traffic_sign
or (highway and highway !~ crossing|traffic_signals|bus_stop|turning_circle)
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

## Information boards

<details><summary>Expand</summary>

### Filtering details

```
tourism = information
and information = board
```

- [x] nodes
- [ ] ways
- [ ] relations

### Coloring details

```
board_type
```

- Highlight missing data: No

```

```

</details>

## Bicycle parking

<details><summary>Expand</summary>

### Filtering details

```
amenity=bicycle_parking
```

- [x] nodes
- [x] ways
- [x] relations

### Coloring details

```
bicycle_parking|capacity|covered|access|fee
```

- Highlight missing data: Yes

```

```

</details>
