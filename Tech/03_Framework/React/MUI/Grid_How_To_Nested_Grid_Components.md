# How to nested `<Grid>` components with proper spacing

## Solution:

    A `<Grid>` tag to have an `item` AND `container` property, they should be nested like `Grid[container] => Grid[item] => Grid[container]`.

## Demo:

```javascript
<Grid
	container
	spacing={3}
	direction="row"
	justify="center"
	alignItems="center"
>
	<Grid item direction="row" justify="center" alignItems="center" xs={8}>
		<Grid container spacing={3}>
			<Item />
			<Item />
			<Item />
		</Grid>
	</Grid>

	<Grid item direction="row" justify="center" alignItems="center" xs={4}>
		<Grid container spacing={3}>
			<Item />
			<Item />
		</Grid>
	</Grid>

	<Grid item direction="row" justify="center" alignItems="center" xs={12}>
		<Item />
	</Grid>
</Grid>
```

---

## References:

- [Material-ui nested grids margins](https://stackoverflow.com/questions/59992924/material-ui-nested-grids-margins)
