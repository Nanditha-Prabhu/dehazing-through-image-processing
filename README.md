# Dehazing through Image Processing

## Problem Statement
To develop effective image processing techniques for dehazing hazy images captured in outdoor scenes.

## Algorithms Used
- **Histogram Equalization Algorithm (equalize_histogram function):**
  - Input: Grayscale image (numpy array).
  - Output: Histogram equalized grayscale image (numpy array).
  - Steps:
    - Compute the histogram of pixel intensities.
    - Calculate the cumulative distribution function (CDF) of the histogram.
    - Normalize the CDF.
    - Interpolate the pixel intensities using the normalized CDF.
    - Scale the pixel intensities to the range [0, 255].
    - Reshape the equalized pixel intensities to the original image shape.
  - Observation:  The output image obtained after performing Histogram Equalization had improved the contrast in an image by redistributing the pixel intensity values thereby producing a brighter image than the expected normal image.
    
- **CLAHE (Contrast Limited Adaptive Histogram Equalization) Algorithm (apply_clahe_function):**
  - Input: RGB image (numpy array).
  - Output: CLAHE enhanced RGB image (numpy array).
  - Steps:
    - Split the RGB image into individual color channels.
    - Apply CLAHE to each color channel independently.
    - Merge the CLAHE enhanced color channels back into a single RGB image.
  - Observation: CLAHE is a better version of histogram equalization that helps in enhancing the local contrast of the input image by redistributing the brightness values within small regions (tiles) of the image. This allowed details in both dark and bright areas to become more visible producing a realistic image.
  - **Repeated CLAHE with unsharp masking**: The images obtained after performing CLAHE and unsharp masking gives better results as the haze is removed , enabling us to clearly view the sun set, clouds, river and the rock structure which was not possible by CLAHE applied Gamma correction.
  
- **Unsharp Masking Algorithm (apply_unsharp_mask function):**
  - Input: RGB image (numpy array).
  - Output: Sharpened RGB image (numpy array).
  - Steps:
    - Apply Gaussian blur to the input image.
    - Subtract the blurred image from the original image to obtain the high-pass filtered image.
    - Scale the high-pass filtered image and add it back to the original image to obtain the sharpened image.
  - Observation:  Applying unsharp masking to the hazed image produced an image with edges and fine details appearing more pronounced making it more darker. Unsharp masking can be used effectively after performing histogram equalization methods like CLAHE.
  
- **Gamma Correction Algorithm (apply_gamma_correction function):**
  - Input: RGB image (numpy array).
  - Output: Gamma corrected RGB image (numpy array).
  - Steps:
    - Normalize the input image intensities to the range [0, 1].
    - Apply gamma correction to adjust the brightness and contrast of the
    image.
    - Scale the pixel intensities back to the range [0, 255].
    - Convert the gamma corrected image to uint8 format.
  - Observation: By performing Gamma Correction to CLAHE, the obtained image produced desired output for the input images that had haze evenly distributed. While the results obtained for images with uneven haze distribution was not satisfactory.
  
## Conclusion
In conclusion, the developed dehazing pipeline has proven to be highly effective in removing haze and enhancing the quality of hazy images. Pipeline with CLAHE followed by Gamma Correction worked well for images with uniform distribution of haze whereas pipeline with CLAHE followed by Unsharp masking worked well for unevenly distributed haze as well. Through rigorous experimental evaluation, the algorithm demonstrated significant improvements in visual clarity. Moreover, the algorithm exhibited efficient computational performance, making it suitable for practical applications in image processing and computer vision tasks. Overall, this project has contributed to advancing the field of image enhancement and provides a valuable tool for improving visibility in hazy conditions.
