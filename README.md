# replace-color

Simple html/css/javascript project to change every pixel in an image with a certain color -- to another color.

## Getting Started

Begin by running the files or going to https://watermelonpop.github.io/replace-color/. This should show a website with an upload button, a download button, a revert icon button, color wheel component, and tolerance sliding bar. Use the upload button to upload any image file(works with pngs as well as jpegs). Change the color wheel to the color you wish to change the pixels to. You can choose a tolerance using the sliding bar, which determines how big the range is of acceptably colored pixels. Then click on any color in the image to change every instance of that color to the new color from the color wheel. You can then revert the image to the original to work with a new slate, or download the image to your computer using the download button.

## Usage

Uses bootstrap, coloris, and fontawesome as helpers for our website. Bootstrap for css purposes, coloris for the color wheel functionality, and fontawesome for the icons used in the project.

When the input image has changed, draw the image on the canvas. 
When the user clicks on a color, need to keep the location and color of the click, and change every pixel accordingly.
When the user clicks the download button, the image should download to their computer under the name: "color-replaced". 
When the user changes the tolerance, the next time they click on a color in the image, the fill tolerance will be adjusted.
When the user clicks the revert icon button, the canvas should show the original image uploaded.

## Global Variables
```javascript
var inputImg = document.getElementById('uploadInput');
  // this links the code to the input component in the html
  // we can use this to get the image data, so we can manipulate it
var canvas = document.getElementById('Canvas');
var context = canvas.getContext('2d');
  //basic variables needed for javascript canvas
var newColor = '000000';
  // the "new color" that we want to transform our pixels into
  // the default new color is black
var tolerance = 100;
  // tolerance level default is 100
  // we'll use this variable to track the tolerance level of the sliding bar
var oldImg;
  // olds the original image, so that the revert button can restore the original
```
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
## Main Function - changePixels(x, y, color, tol)
Function input:
- x
  - x-coordinate of the click
- y
  - y-coordinate of the click
- color
  - new color inputted through the color wheel (this is the color we want to transform our pixels into)
- tol
  - tolerance level taken from the sliding tolerance bar (we use this in our range of acceptable matching pixel colors)

The function gets image data from the canvas, where drawImg() has already placed the image. Then uses getPixel() with the image data, x, and y to get the "old color" that we want to replace. We already have our "new color" from the function arguments. Then the image data is traversed with a nested for-loop. At each pixel, the rgba, and therefore hex code is found. As long as the pixel is NOT transparent, we use colorsMatch() to check if the current pixel color is the same as the "old color" that we want to isolate. If these colors do match, then we change the pixel color to be the "new color". This is repeated through every pixel. At the very end, the new image data is applied to the canvas, and displayed to the user. 
```javascript
function changePixels(x, y, color, tol){
        const imgData = context.getImageData(0, 0, canvas.width, canvas.height);
        const data = imgData.data;
        let oldColor = getPixel(imgData, x, y);
        
        for(let row = 0; row < canvas.height; row++){
                for(let col = 0; col < canvas.width; col++){
                        let index = (col + (row * imgData.width))*4;
                        let r = imgData.data[index];
                        let g = imgData.data[index + 1];
                        let b = imgData.data[index + 2];
                        let a = imgData.data[index + 3];
                        let hex = rgbToHex(r, g, b, a);
                        if(hex != '-1'){
                                if(colorsMatch(hex, oldColor, tol*tol)){
                                        let newRgb = hexToRgb(color);
                                        imgData.data[index] = newRgb[0];
                                        imgData.data[index + 1] = newRgb[1];
                                        imgData.data[index + 2] = newRgb[2];
                                }
                        }
                }
        }
        
        context.putImageData(imgData, 0, 0);
}
```
