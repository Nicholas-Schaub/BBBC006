Source: https://data.broadinstitute.org/bbbc/BBBC006/
Citation: Bray, M.-A., Fraser, A. N., Hasaka, T. P., & Carpenter, A. E. (2012).
          Workflow and Metrics for Image Quality Control in Large-Scale
          High-Content Screens. Journal of Biomolecular Screening, 17(2),
          266–274. https://doi.org/10.1177/1087057111420292

------------
Data Summary
------------
U2OS cells were cultured in a 384 well plate. Two images were captured per well
in two different channel (w1=DAPI/nuclei, w2=phalloidin/cytoskeleton). Images
were captured at different focal planes, and images in each zip file contain all
fields of view captured in a single focal plane. The zip file ending with _z_16
is considered in focus, and values smaller than that are below the focal plane
(e.g. _z_15) and values higher are above the focal plane. Focal planes were
captured 2um apart, so that images in _z_15 were captured 2um below the position
of images in _z_16.

------------
Ground Truth
------------
Each image has two pieces of ground truth.
1. The total number of cells in the image (found in BBC006_v1_counts.csv)
2. The nuclei segmentation images (binary images in BBC006_v1_labels)

Note: The nuclei segmentation images are the positions of the nuclei for the
      in-focus plane (_z_16)

-------
Factors
-------
Zip files are named according to focal plane. The focal plane can be extracted
from the file names using the following regular expression
regex -> BBBC006_v1_images_z_([\d]+)

The focal plane relative to the in-focus plane can be determined by taking the
z-plane from the above regular expression and placing it into the following
expression:
RelativeFocalPlane = (z-16)*2        // z is the group extracted from the regex above

The filenames inside of each folder indicate the well and channel that the image
was collected in, the site within the well, and the channel.
To extract the well, site, and channel from the filename:
regex -> mcf-z-stacks-03212011_([A-Za-z0-9]+)_s([0-9])_w([0-9])
Group 1 - well name, contains a letter and number (e.g. a11)
Group 2 - Site number, will be either 1 or 2
Group 3 - Channel number, will be either 1 (nuclei) or 2 (cytoskeleton)

The filenames for the labeled images are slightly different. The following
regular expression can be used to extract info from the filename:
regex -> mcf-z-stacks-03212011_([A-Za-z0-9]+)_s([0-9]).png
Group 1 - well name, contains a letter and number (e.g. a11)
Group 2 - Site number, will be either 1 or 2
