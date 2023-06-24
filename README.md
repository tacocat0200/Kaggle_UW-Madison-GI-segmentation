# UW-Madison GI Tract Image Segmentation

![UW-Madison Logo](uw_madison_logo.png)

## Overview
In 2019, an estimated 5 million people worldwide were diagnosed with cancer of the gastro-intestinal tract. Radiation therapy is a common treatment option, aiming to deliver high doses of radiation to tumors while avoiding the stomach and intestines. However, the manual outlining of the stomach and intestines in daily MRI scans is time-consuming and labor-intensive. This competition focuses on automating the segmentation process using deep learning techniques.

The goal of this competition is to develop a model that can automatically segment the stomach and intestines on MRI scans. The provided dataset consists of MRI scans from actual cancer patients who had 1-5 scans on separate days during their radiation treatment. By leveraging creative deep learning solutions, participants are expected to enhance cancer patients' care and treatment experience.

The University of Wisconsin-Madison (UW-Madison) Carbone Cancer Center, a pioneer in MR-Linac based radiotherapy, supports this project by providing anonymized MRI scans of patients treated at their center. UW-Madison has been treating patients with MRI guided radiotherapy based on their daily anatomy since 2015. The Wisconsin Idea, the university's pledge to the state, the nation, and the world, ensures that their endeavors benefit all citizens.

## Evaluation Metrics
This competition evaluates submissions based on two metrics: the mean Dice coefficient and the 3D Hausdorff distance. The mean Dice coefficient measures the pixel-wise agreement between the predicted segmentation and the ground truth. The 3D Hausdorff distance calculates the distance between segmentation objects by determining the furthest point on one object from the nearest point on the other. The leaderboard score is a combination of these two metrics, with a weight of 0.4 for the Dice coefficient and 0.6 for the Hausdorff distance.

## Submission Format
To submit your results, generate a `submission.csv` file following the provided format. The submission file should use run-length encoding on the pixel values to reduce its size. Instead of listing all indices for your segmentation, submit pairs of values representing the start position and run length. For example, '1 3' implies starting at pixel 1 and running a total of 3 pixels (1, 2, 3). The mask should be binary, with 0 indicating non-masked pixels and 1 indicating masked pixels. The submission file must be named `submission.csv`.

The competition platform checks that the pairs in the submission file are sorted, positive, and do not contain duplicate pixel values. The pixels are numbered from top to bottom, then left to right, starting from 1 as the top-left pixel.

## Getting Started
1. Clone this repository using the following command:

2. Set up the necessary dependencies and libraries to run the code.

3. Download the provided dataset from the competition platform and place it in the appropriate location. The dataset includes MRI scans of cancer patients who underwent 1-5 scans on different treatment days.

4. Run the provided Jupyter Notebook `GI_Tract_Segmentation.ipynb` to train and evaluate your segmentation model. Make sure to adhere to the competition guidelines, including the run-time limits and internet access restrictions.

5. Generate the `submission.csv` file in the required format and save it in the root directory of the repository.

6. Commit and push your changes to the GitHub repository.

## Additional Resources



--------------------------------------------


## Data Description

In this competition, we are provided with images of organs and their corresponding annotations in RLE-encoded masks. The images are in 16-bit grayscale PNG format.

Each case in the competition consists of multiple sets of scan slices, identified by the day the scan took place. Some cases are split by time, where early days are in the training set and later days are in the test set. Other cases are split by case, with the entirety of the case either in the training or test set. The goal is to build a model that can generalize to both partially and wholly unseen cases.

It is important to note that the test set is entirely unseen, consisting of approximately 50 cases with a varying number of days and slices, similar to the training set.

### Hidden Test Set

The test set in this competition is only available when your code is submitted. The provided `sample_submission.csv` file serves as an empty placeholder with the required submission format. Your modeling, cross-validation, and other processes should be performed using the training set. You need to write code to process a non-empty sample submission, which will contain rows with `id`, `class`, and `predicted` columns as described in the Evaluation page.

When you submit your notebook, your code will be run against the non-hidden test set, which follows the same folder format (`<case>/<case_day>/<scans>`) as the training data.

### Files

- `train.csv`: Contains the IDs and masks for all training objects.
- `sample_submission.csv`: A sample submission file in the correct format.
- `train` folder: Contains case/day folders, each containing slice images for a particular case on a given day.

Please note that the image filenames in the `train` folder include four numbers (e.g., `276_276_1.63_1.63.png`). These numbers represent slice width/height (integers in pixels) and width/height pixel spacing (floating points in mm). The first two numbers define the resolution of the slice, while the last two record the physical size of each pixel.

The physical pixel thickness in the superior-inferior direction is 3mm.

### Columns

The provided data has the following columns:

- `id`: Unique identifier for the object.
- `class`: The predicted class for the object.
- `segmentation`: RLE-encoded pixels for the identified object.

