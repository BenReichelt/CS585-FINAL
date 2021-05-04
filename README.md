# CS585-FINAL
A repo for our CS585 groups project on Style Transfer.

Our topic is style transfer. An optimization technique taking two images: Content image (a face) and a Style reference image (an art piece)
The algorithm blends them together so the output image looks like the content image, but portrayed in the style of the style reference image. 

CODE DESCRIPTION: 
- This code first imports necessary packages and defines helper functions to crop and center input images so that the style transfer algorithm can be properly run on them. 

- We then have a cell where the MSE and SSIM algorithm functions are defined, as well as the TensorFlow hub module. 

- Next we define our arrays of content image URLs, all organized into different classifications to be used for later testing.

- The next cell is a image tester to make sure both URLs are able to have their corresponding image load correctly.

- A function called styleDriver that is essentially the function that pulls all of the other parts of the code together, and actually runs the style transfer algorithm. 

- styleDriver runs the style transfer on the given images, and does 4 combinations of MSE and SSIM calculations,
  -  grayscale content vs. stylized output
  -  color content vs. stylized output
  -  grayscale style vs. stylized output
  -  color style vs. stylized output
  
  The MSE and SSIM values from each 4 of these calculations are averaged and we used these averages to compare the effectiveness of style transfer between images.

- Finally there is a cell containing a loop to facilitate running styleDriver on a set of content URLs
  - This prints out a picture of the content image, the style image, and the stylized output image
  - Below the avg MSE and SSIM for this style transfer is printed as MAVG and SAVG respectively.

TO USE:
1. Upload ipynb to google COLAB.
2. Run first cell on ipynb to import everything necessary and build helper functions.
3. Next run data set arrays cell.
4. Next run styleDriver().
5. Next define the set you wish to analyze in the "for loop" at the bottom.
6. Analyze results 


EXAMPLE:

![Screen Shot 2021-04-30 at 7 09 22 PM](https://user-images.githubusercontent.com/61470389/116762164-95298d80-a9e7-11eb-9760-09c9178fa5a4.png)

![Screen Shot 2021-04-30 at 7 07 42 PM](https://user-images.githubusercontent.com/61470389/116762078-58f62d00-a9e7-11eb-98a3-cb55c0eee3cc.png)

DISCUSSION OF RESULTS:
- COLOR : 
    - White and dark/black backgrounds → lowest similarity (less successful)
    - Green and grey backgrounds → highest similarity (more successful)
    - Color similarities are captured in the our measurement of color content and color style comparisons in MSE and SSIM error values. 
    
    These similarity averages result in green and grey background content images having the highest similarity to the output image when given colorful style images,
    whose colors also average to mid range RGB values (like green and lighter grey). The least similar scores being found on content images with white backgrounds 
    or large sections of black in backgrounds also makes sense, as these averages are at the furthest end of the range of color values at 0 and 255. 
    
 - Texture:
    - Textured content image + textured style → high similarity (more successful) →  Van Gogh
    - Smooth/gradient background + smooth style → high similarity (more successful) → Harrington and O’Keefe
    - Mismatches in background + style texture→ low similarity (less successful)

    Using the greyscale content and greyscale style comparisons, our methods capture texture through contour comparisons in MSE and SSIM error values. 
    In the Van Gogh style, which had a more consistent pattern and texture, the best matches were images that had green and grey backgrounds, albeit ones with
    texture (leaves, shapes, etc), rather than a smooth gradient like Harrington and O’Keeffe. 
    This shows the algorithm, as well as our method for measuring 
    similarity, is more successful (in terms of transferring style while also maintaining the content) on similar textured backgrounds to the style of the image. 

- Limitations:
    - Our style images are all relatively colorful, using more grayscale styles might’ve given us more information on how well the algorithm works on varying style colors.
    - As well, a wider range of art styles in general would give us more information.
    - However, in only our 3 art styles, we had over 90 datasets, each with 4 measurement outputs. This means adding another style would’ve significantly scaled our dataset to less manageable proportions.

