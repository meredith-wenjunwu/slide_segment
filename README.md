# Data Preprocessing and Post-processing

### List of Files

`slide_segment.py` Supporting functions that separates the slices in a biospy image

### Prepare data

1. prepare the slides in lower resolution for slide segmentation (recommended x2.5)
2. Openslide sample command for one image

```Python
slide = openslide.OpenSlide('900.ndpi')
#check which zoom level you want to get
#in this case, zoom x2.5 is level 4
slide_x2_5 = slide.read_region((0,0), 4, slide.level_dimensions[4]).convert('RGB')
slide_x2_5.save('900_x2.5.tif')
```

### Slide Segmentation

The following command runs a single image:

```Python
python slide_segment.py --input_image 'original/1/MP_0169_x2.5_z0.tif' --output_path 'melanoma_diagnosis/mpathx2.5/1/' --create_overlay True --distance_threshold 50 --area_threshold 8000
```

The following command runs the entire folder of class 2:

```Python
python slide_segment.py --input_folder 'original/3/' --output_path 'melanoma_diagnosis/mpathx2.5/2/' --create_overlay True --distance_threshold 50 --area_threshold 8000
```

This will create separate images for each slice and a csv file with the bounding box of each slice (under x2.5 zoom). 

