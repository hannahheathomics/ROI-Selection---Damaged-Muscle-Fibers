# Damaged Muscle ROI Selector

Crops square ROIs from fluorescence muscle cross-section images for cross-sectional area (CSA) analysis, targeting regions with damaged muscle fibers.

---

## Overview

| | |
|---|---|
| **Input** | RGB/RGBA PNG — Green = Laminin, Blue = DAPI |
| **Output** | Single-channel laminin TIFF (uint8) + RGB QC preview TIFF with yellow ROI box |

---

## ROI Selection Logic

1. Identifies the largest tissue region from the combined green/blue signal
2. Applies an edge margin to exclude edge fibers from the search zone
3. Measures actual tissue density across the interior and requires each candidate ROI to meet at least 70% of that value
4. Slides a square window across the interior to find the patch with the highest mean laminin signal within tissue pixels

> Higher laminin density per unit area = more cell borders = smaller/damaged fibers

---

## Troubleshooting

Individual images can be re-run with adjusted parameters to correct for common failure cases, such as excess background inclusion or non-muscle-fiber inclusion.
