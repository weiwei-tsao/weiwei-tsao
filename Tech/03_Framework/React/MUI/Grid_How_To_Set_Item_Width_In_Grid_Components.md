# How to set item width in `<Grid>` components

## Solution:

    Using [fluid grid property](https://material-ui.com/customization/breakpoints/), this property only works on item elements, not on container. The padding between items is setting in contaner using `spacing` keyword

    `xs` Defines the number of grids the component is going to use. It's applied for **all the screen sizes** with the lowest priority.

    `sm` Defines the number of grids the component is going to use. It's applied for the sm breakpoint and wider screens if not overridden.

    `md` Defines the number of grids the component is going to use. It's applied for the md breakpoint and wider screens if not overridden.

## Demo:

Refer to [How to nested `<Grid>` components with proper spacing](https://github.com/weiwei-tsao/weiwei-tsao/blob/main/Tech/03_Framework/React/MUI/Grid_How_To_Nested_Grid_Components.md)

---

## References:

- [Full Width Material-UI Grid not working as it should](https://stackoverflow.com/questions/49797264/full-width-material-ui-grid-not-working-as-it-should)
- [The MUI grid system](https://blog.logrocket.com/mui-grid-system/)
