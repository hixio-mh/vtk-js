Representations are scene objects that render based on the attached widget
state. These are not to be instantiated directly; rather, these should be
referenced in an implementation of
`vtkAbstractWidgetFactory.getRepresentationsForViewType`.


Look at `vtkContextRepresentation` and `vtkHandleRepresentation` for more usable
base classes.

## getRepresentationStates(inputState)

This will return a list of all states that match against the list of labels set
via `setLabels(...labels)`.

## setLabels(...labels)

Used internally to set the target labels. When requestData is invoked,
`getRepresentationStates(inData[0])` can be used to retrieve the list of states
that match the target labels.

## addActor(actor)

Should be used when creating an actor for the representation. It will apply widget-wide configuration such as coincident topology parameters to the mapper.

## getDisplayScaleAtCoord(coord)

`getDisplayScaleAtCoord(coord)` will return some scaling to be applied to a
widget representation. What it returns depends on what flags are set. If
`model.scaleByDisplay=true` and `model.scaleInPixels=false`, the method will
return the viewport height in world coordinates at a particular point. In other
words, it is the height of the rectangle formed by the intersection of the
plane (defined by the camera normal and the provided coord) and the view
frustrum. In this mode of operation, representations will typically treat
properties like `scale1` to be a fraction of the viewport height.

When `model.scaleByDisplay=true` and `model.scaleInPixels=true`,
`getDisplayScaleAtCoord(coord)` returns a (vertical) world distance that
corresponds to a single pixel in display space. Representations will typically
treat properties like `scale1` to be the height of the representation in pixel
values.
