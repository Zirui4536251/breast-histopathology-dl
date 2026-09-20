# Data specification and provenance

## Source

The assignment describes H&E-stained breast tissue images collected from mastectomy or biopsy specimens, at 0.25 micrometres per pixel. Images were distributed through NTULearn as `HW6training.zip`, `HW6validation.zip`, and `HW6testing.zip`.

**The original public dataset, publication, image provider and redistribution licence are not specified in the supplied assignment or notebook.** This repository does not attribute the images to TCGA, BACH, BreakHis or another named dataset. NTULearn is the course distribution channel, not an identified original image source.

The specification below comes from the assignment and notebook, not a new inspection of raw image files. Raw images and the trained checkpoint are not included. The saved Grad-CAM panels contain course image examples already embedded in the submitted notebook; their underlying image rights remain unspecified. Check course policy and image permissions before making those panels public.

## Expected layout

Place the extracted folders under `data/raw/`:

| Relative directory | Content | Assignment count |
| --- | --- | ---: |
| `HW6training/0_N/` | Normal tissue, label 0 | 338 |
| `HW6training/1_IC/` | Invasive carcinoma, label 1 | 352 |
| `HW6validation/0_N/` | Normal tissue, label 0 | 35 |
| `HW6validation/1_IC/` | Invasive carcinoma, label 1 | 47 |
| `HW6testing/` | Unlabeled images | 149 |

## Image and label conventions

- Assignment image dimensions: 512 × 512 pixels, three colour channels.
- The loader converts images to RGB. Model inputs are resized to 224 × 224 and normalized using ImageNet channel statistics.
- Labeled-image loading accepts `.png`, `.jpg`, and `.jpeg`; the test loader also accepts `.tif` and `.tiff`. Extension matching in the original code is case-sensitive.
- The training pool is split at image level into 552 training and 138 internal-validation images. The separately supplied 82-image validation folder is evaluated afterwards.
- Test identifiers span UK1 to UK162 with gaps; there are 149 actual images. The original code sorts by the numeric identifier, rather than lexicographically.
- Patient IDs, slide IDs, acquisition centres, and patient-level split information were not supplied in the materials reviewed. Patient independence across splits cannot be established.

There is no verified public download link to provide. Obtain the images through the authorized course distribution or clarify provenance with the course instructor. Do not substitute another dataset and describe its results as this original run.
