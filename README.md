 Example of using Helm and Argo string interpolation together.

# The Broken Chart

[broken-chart](broken-chart) is an unmodified Argo manifest, packaged as a Helm Chart.
`helm install broken-example ./broken-chart` will fail, because Helm tries to interpolate a value meant for Argo.

# The Fixed Chart

[working-chart](working-chart) is the same manifest, modified to use `{-` and `-}` as Argo delimiters.
[argo-post-processor.sh](argo-post-processor.sh) is post renderer script for Helm that converts the new delimiters
back to the `{{` and `}}` syntax Argo expects after Helm is done.
`helm install fixed-example ./working-chart --post-renderer ./argo-post-processor.sh`
installs the chart without error,
interpolating a value from Helm and rendering the Argo delimiters correctly in the final output.
