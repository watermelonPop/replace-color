# replace-color

Simple html/css/javascript project to change every pixel in an image with a certain color -- to another color.

## Getting Started

Begin by running the files or going to https://watermelonpop.github.io/replace-color/. This should show a website with an upload button, a download button, a revert icon button, color wheel component, and tolerance sliding bar. Use the upload button to upload any image file(works with pngs as well as jpegs). Change the color wheel to the color you wish to change the pixels to. You can choose a tolerance using the sliding bar, which determines how big the range is of acceptably colored pixels. Then click on any color in the image to change every instance of that color to the picked color from the color wheel. You can then revert the image to the original to work with a new slate, or download the image to your computer using the download button.

## Usage

Uses bootstrap, coloris, and fontawesome as helpers for our website. Bootstrap for css purposes, coloris for the color wheel functionality, and fontawesome for the icons used in the project.

When the input image has changed, draw the image on the canvas. 
When the user clicks on a color, need to keep the location and color of the click, and change every pixel accordingly.
When the user clicks the download button, the image should download to their computer under the name: "color-replaced". 
When the user changes the tolerance, the next time they click on a color in the image, the fill tolerance will be adjusted.
When the user clicks the revert icon button, the canvas should show the original image uploaded.

## Useful helper functions used: 
```javascript
- changeNewColor(c)
  // Updates the variable of the new color based on changes in the color wheel.
- drawImg()
  // Draws the image to the canvas.
- getPixel(imageData, x, y)
  // Takes in image data, and x and y coordinates of the click, outputs the color of the clicked pixel.
- colorsMatch(a, b, rangeSq)
  // Takes in colors a and b, and the acceptable range taken from the tolerance bar. 
  // Outputs whether the 2 colors match(true) or dont match(false).
- colorToHex(color)
  // Changes hex code into color array(rgba)
- rgbToHex(r, g, b, a=1)
  // Converts rgba values to hex codes.
  // rgba colors have levels of transparency, while hex codes do not. 
  // This is why if the rgba value is transparent, -1 is returned rather than a hex code.
- hexToRgb(hex)
  // Converts hex codes into color array(rgba)
- getElementPosition(obj)
  // gets the x and y coordinates of an element
- getEventLocation(element, event)
  // uses getElementPosition() to get x and y coordinates of a click.
```
## Main Function


## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.
