I've tried to make design files available in a wide variety of formats to support editing and redesign as needed:

1. `fusion/` contains fusion 360 files for complete control over the timeline and features for editing
2. `step/` contains step files for non-meshified exports which better preserve the underlying geometry for minor tweaks and portability outside of fusion
3. `stl/` contains exported meshes, which are not great for editing, but are convenient for printing
4. `dxf/` contains outlines which you can use to start a new case design from scratch. See [the case design docs](/docs/case-design.md#shadow-line) for some notes on the generated outlines (and why you may want to export something different from ergogen, depending on your use case)

The exported case files are generally going to follow one of the three naming schemes:

- `bottom`: this is the simplest case -- there's just one common bottom for all cases, so there's no variants to track. Fusion and step files will have one common file for both halves, whereas stl will export a left and right separately.
- `top_${layout}`: where layout is be one of `3x5_3`, `3x5_2`, `23332_2` etc. For stls, there's again left and right exports, as well as exports for variants with `no-rst`, no cutout for the reset button
- `wedge_${angle}_${distance}_${feature}`: the angle refers to the angle between a keyboard half and the vertical, and the distance refers to the distance between the top corners of the keyboard halves. The (optional) feature represents any peripheral you may mount in the wedge, like a cirque trackpad.
