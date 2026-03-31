**Purpose:** Crops square ROIs from fluorescence muscle cross-section images for CSA analysis, specifically focusing on areas with damaged muscle fibers.

- Input: RGB/RGBA PNG (Green = Laminin, Blue = DAPI)
- Output: Single-channel laminin TIFF (uint8) + RGB QC preview TIFF with yellow ROI box

ROI selection logic: Identifies the largest tissue region (green/blue signal) and applies an edge margin to avoid capturing edge fibers. For each image, the algorithm determines how much of the interior search zone is actual tissue, then requires each candidate ROI contain at least 70% of total tissue area. A square window then slides across the interior to find the patch with the highest mean laminin signal within tissue pixels. The idea is that higher laminin density per unit area = more cell borders = smaller/damaged fibers.

Troubleshooting: Individual images can be re-run with adjusted parameters to correct for common failure cases: nerve/connective tissue fragments that outscore the muscle (corrected via blue-channel exclusion), and excess background inclusion (corrected via stricter tissue threshold and larger edge margin).
