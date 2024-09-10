# Project1

## Colorizing the Prokudin-Gorskii photo collection

### Single-scale version (for small image)

I use the L2 norm metric and search over a window of [-15, 15] to align the G and R channels to the B channel. Also, I crop the image by 10% on each side for a better alignment.

Below are the results for all `.jpg` images.

<div style="display: flex; flex-wrap: wrap;">
  <div style="margin: 10px;">
    <img src="cathedral_output.jpg" alt="Cathedral" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="monastery_output.jpg" alt="Monastery" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="tobolsk_output.jpg" alt="Tobolsk" width="300"/>
  </div>
</div>

### Multi-scale version (for all images)

I keep using the L2 norm metric and add a coarse-to-fine pyramid to speed up processing for large images like `.tif` images.

Below are the results for all `.tif` and `.jpg` images.

<div style="display: flex; flex-wrap: wrap;">
  <div style="margin: 10px;">
    <img src="cathedral_output.jpg" alt="Cathedral" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="monastery_output.jpg" alt="Monastery" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="tobolsk_output.jpg" alt="Tobolsk" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="church_output.jpg" alt="Church" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="emir_output.jpg" alt="Emir" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="harvesters_output.jpg" alt="Harvesters" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="icon_output.jpg" alt="Icon" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="lady_output.jpg" alt="Lady" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="melons_output.jpg" alt="Melons" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="onion_church_output.jpg" alt="Onion Church" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="sculpture_output.jpg" alt="Sculpture" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="self_portrait_output.jpg" alt="Self Portrait" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="three_generations_output.jpg" alt="Three Generations" width="300"/>
  </div>
  <div style="margin: 10px;">
    <img src="train_output.jpg" alt="Train" width="300"/>
  </div>
</div>
