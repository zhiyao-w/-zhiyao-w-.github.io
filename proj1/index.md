# Project1

## Colorizing the Prokudin-Gorskii photo collection

### single-scale version (for small image)
I use the L2 norm metric and search over a window of [-15, 15] to align the G and R channels to the B channel. Also I crop the image off for 10% on each side for a better alignment.

Below are the results for all .jpg image.
![cathedral](cathedral_output.jpg)
![monastery](monastery_output.jpg)
![tobolsk](tobolsk_output.jpg)

### multi-scale version (for all image)
I keep using the L2 norm metric, and add a coarse-to-fine pyramid to speed up when processing large image like .tif image.

Below are the results for all .jpg image.
![cathedral](cathedral_output.jpg)
![monastery](monastery_output.jpg)
![tobolsk](tobolsk_output.jpg)
![church](church_output.jpg)
![emir](emir_output.jpg)
![harvesters](harvesters_output.jpg)
![icon](icon_output.jpg)
![lady](lady_output.jpg)
![melons](melons_output.jpg)
![onion_church](onion_church_output.jpg)
![sculpture](sculpture_output.jpg)
![self_portrait](self_portrait_output.jpg)
![three_generations](three_generations_output.jpg)
![train](train_output.jpg)
