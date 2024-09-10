# Project1

## Colorizing the Prokudin-Gorskii Photo Collection

### Single-scale Version (for Small Images)

I use the L2 norm metric and search over a window of [-15, 15] to align the G and R channels to the B channel. Also, I crop the image by 10% on each side at the begining for better alignment.

Below are the results for all `.jpg` images:

<table>
  <tr>
    <td align="center">
      <img src="cathedral_output.jpg" alt="Cathedral" width="300"><br>
      <b>Cathedral</b>
    </td>
    <td align="center">
      <img src="monastery_output.jpg" alt="Monastery" width="300"><br>
      <b>Monastery</b>
    </td>
    <td align="center">
      <img src="tobolsk_output.jpg" alt="Tobolsk" width="300"><br>
      <b>Tobolsk</b>
    </td>
  </tr>
</table>

### Multi-scale Version (for All Images)

I continue using the L2 norm metric and add a coarse-to-fine pyramid to speed up processing for large images like `.tif` images.

Below are the results for all images:

<table>
  <tr>
    <td align="center">
      <img src="cathedral_output.jpg" alt="Cathedral" width="300"><br>
      <b>Cathedral</b>
    </td>
    <td align="center">
      <img src="monastery_output.jpg" alt="Monastery" width="300"><br>
      <b>Monastery</b>
    </td>
    <td align="center">
      <img src="tobolsk_output.jpg" alt="Tobolsk" width="300"><br>
      <b>Tobolsk</b>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="church_output.jpg" alt="Church" width="300"><br>
      <b>Church</b>
    </td>
    <td align="center">
      <img src="emir_output.jpg" alt="Emir" width="300"><br>
      <b>Emir</b>
    </td>
    <td align="center">
      <img src="harvesters_output.jpg" alt="Harvesters" width="300"><br>
      <b>Harvesters</b>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="icon_output.jpg" alt="Icon" width="300"><br>
      <b>Icon</b>
    </td>
    <td align="center">
      <img src="lady_output.jpg" alt="Lady" width="300"><br>
      <b>Lady</b>
    </td>
    <td align="center">
      <img src="melons_output.jpg" alt="Melons" width="300"><br>
      <b>Melons</b>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="onion_church_output.jpg" alt="Onion Church" width="300"><br>
      <b>Onion Church</b>
    </td>
    <td align="center">
      <img src="sculpture_output.jpg" alt="Sculpture" width="300"><br>
      <b>Sculpture</b>
    </td>
    <td align="center">
      <img src="self_portrait_output.jpg" alt="Self Portrait" width="300"><br>
      <b>Self Portrait</b>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="three_generations_output.jpg" alt="Three Generations" width="300"><br>
      <b>Three Generations</b>
    </td>
    <td align="center">
      <img src="train_output.jpg" alt="Train" width="300"><br>
      <b>Train</b>
    </td>
    <!-- Add more images here if needed -->
  </tr>
</table>
