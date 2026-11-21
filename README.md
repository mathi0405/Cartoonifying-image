# Cartoonify an image (OpenCV)

A small desktop tool that turns a photo into a cartoon-style image with classical
image processing, no neural network involved. A Tkinter window lets you pick an image, shows
every step of the transformation, and saves the result next to the original.

## How it works

1. Read the image and convert it to RGB.
2. Convert to grayscale and smooth it with a 5×5 median blur.
3. Extract edges with adaptive mean thresholding (block size 9, C = 9).
4. Flatten the colours with a bilateral filter (d = 9, σ = 300), which keeps edges sharp.
5. Combine: the colour image is masked with the edge map (`bitwise_and`).

The notebook plots all six stages (original, gray, blurred, edges, filtered colour, cartoon).

## Run

```bash
pip install opencv-python numpy matplotlib imageio easygui pillow
jupyter notebook "Cartoonifying image.ipynb"
```

Run the cell, click **Upload**, choose an image, then **Save cartoon image**. The file
is saved as `cartoonified_Image.<ext>` in the image's folder. It needs a desktop
session because it opens Tkinter/easygui windows.

## Changelog
- 2026-11: the missing-image check now runs before the colour conversion (previously
  an invalid path raised an OpenCV error instead of the message), and grayscale
  conversion uses the RGB order the image is stored in.
