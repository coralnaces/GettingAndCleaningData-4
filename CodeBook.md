# CodeBook

## Introduction

This file is the Code Book for the `run_analysis.R` script.

## Variables

| Variable | Description|
|----------|------------|
| data.dir | Default location for the SAMSUNG data |
| data.tidydir | Name of the output directory |
| data.url | URL of the data archive |
| data.archive | Name of the downloaded archive, inside the `data.dir` folder |
| data.filename | Name of the folder containing the data files (when extracted from the archive) |
| data.test.file.subject | path of the file containing the subjects for the test set |
| data.test.file.x | path of the file containing the variables for the test set |
| data.test.file.y | path of the file containing the outputs (activities) for the test sets |
| data.train.file.subject | path of the file containing the subjects for the train set |
| data.train.file.x | path of the file containing the variables for the train set |
| data.train.file.y | path of the file containing the outputs (activities) for the train sets |
| data.activity_names | Labels corresponding to the activities |
| data.feature_ids | Ids of the columns that are to be extracted |
| data.feature_names | Corresponding names for the columns to be used in the tidy dataset |
| data.feature_names | Corresponding names for the columns to be used in the tidy dataset |
| data.test.data.subject | Content of the subjects file for the test set |
| data.test.data.x | Values of the features from the test set |
| data.test.data.y | Values of the outputs from the test set |
| data.test | Dataset containing all the combined data from the variables `data.test.data.subject`, `data.test.data.x` and `data.test.data.y` |
| data.train.data.x | Values of the features from the train set |
| data.train.data.y | Values of the outputs from the train set |
| data.train | Dataset containing all the combined data from the variables `data.train.data.subject`, `data.train.data.x` and `data.train.data.y` |
| tidy1 | Resulting output containing the tidy dataset (requirements 1 to 4) |
| tidy2 | Resulting dataset containing the grouped average of the features based on activity and subject (requirement 5) |

## Contents of the tidy datasets

| Variable | Description|
|----------|------------|
| subject | The subject of the observation |
| set | The set containing the data (TEST or TRAINING) |
| tbody_accel_mean_x | |
| tbody_accel_mean_y | |
| tbody_accel_mean_z | |
| tbody_accel_std_x | |
| tbody_accel_std_y | |
| tbody_accel_std_z | |
| tgravity_accel_mean_x | |
| tgravity_accel_mean_y | |
| tgravity_accel_mean_z | |
| tgravity_accel_std_x | |
| tgravity_accel_std_y | |
| tgravity_accel_std_z | |
| tbody_accel_jerk_mean_x | |
| tbody_accel_jerk_mean_y | |
| tbody_accel_jerk_mean_z | |
| tbody_accel_jerk_std_x | |
| tbody_accel_jerk_std_y | |
| tbody_accel_jerk_std_z | |
| tbody_gyro_mean_x | |
| tbody_gyro_mean_y | |
| tbody_gyro_mean_z | |
| tbody_gyro_std_x | |
| tbody_gyro_std_y | |
| tbody_gyro_std_z | |
| tbody_gyrojerk_mean_x | |
| tbody_gyrojerk_mean_y | |
| tbody_gyrojerk_mean_z | |
| tbody_gyrojerk_std_x | |
| tbody_gyrojerk_std_y | |
| tbody_gyrojerk_std_z | |
| tbody_accel_mag_mean | |
| tbody_accel_mag_std | |
| tgravity_accel_mag_mean | |
| tgravity_accel_mag_std | |
| tbody_accel_jerkmag_mean | |
| tbody_accel_jerkmag_std | |
| tbody_gyro_mag_mean | |
| tbody_gyro_mag_std | |
| tbody_gyrojerk_mag_mean | |
| tbody_gyrojerk_mag_std | |
| fbody_accel_mean_x | |
| fbody_accel_mean_y | |
| fbody_accel_mean_z | |
| fbody_accel_std_x | |
| fbody_accel_std_y | |
| fbody_accel_std_z | |
| fbody_accel_jerk_mean_x | |
| fbody_accel_jerk_mean_y | |
| fbody_accel_jerk_mean_z | |
| fbody_accel_jerk_std_x | |
| fbody_accel_jerk_std_y | |
| fbody_accel_jerk_std_z | |
| fbody_gyro_mean_x | |
| fbody_gyro_mean_y | |
| fbody_gyro_mean_z | |
| fbody_gyro_std_x | |
| fbody_gyro_std_y | |
| fbody_gyro_std_z | |
| fbody_accel_mag_mean | |
| fbody_accel_mag_std | |
| fbody_body_accel_jerk_mag_mean | |
| fbody_body_accel_jerk_mag_std | |
| fbody_body_gyro_mag_mean | |
| fbody_body_gyro_mag_std | |
| fbody_body_gyro_jerk_mag_mean | |
| fbody_body_gyro_jerk_mag_std | |
| activity | The expected output of the observation |

## Script explanation

To generate a tidy dataset, the script does the following:

### Creates the source and destination folders if they don't exist

### Download the data if not present inside the source folder

### Initialize variables to be used when transforming the data

### Load the files using readLines

As the values are separated by space instead of common csv separator, `readLines` has been used. The features also have some padding before the first value on each row hence the use of the `trimws` function to remove those spaces. The line is then split based on one or more spaces (`str_split` with the pattern `( +)`) and simplified to be a vector.

The datasets are converted into tables (`as_tibble`); correct columns are selected; values are converted into numeric `mutate_all` and then assigned correct column names.

A new `set` column is added to differentiate the sets if needed.

Pipline (`%>%`) is used to eliminate intermediate variables.

Columns are bound to form each sets; and then the sets rows are bound to form the final tidy dataset.

Intermediate variables are removed to free memory space and to avoid confusion.

### Second tidy data is created using grouping (`group_by`) and `summarize`

The `set` column is removed from the summary using `select`.

### Files are written into the output directory
