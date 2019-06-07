# The FPV Drone Racing VIO Competition

The FPV Drone Racing VIO competition will be held jointly with **WORKSHOP NAME** at IROS 2019.

The participants are required to run their VIO algorithms on datasets (including images, IMU measurements and event data) recorded with a FPV drone racing quadrotor flown aggressively by an expert pilot. The goal is to estimate the quadrotor motion as accurately as possible, utilizing any possible sensor combinations. The winner will be selected based on the accuracy of the estimated trajectories (details follow below), and awarded **XX**

Deadline to submit the estimated trajectories and report: **XX**

1. [Datasets](#datasets)
2. [Submission Format](#submission-format)
   * [Estimated Trajectories](#estimated-trajectories)
   * [Report](#report)
3. [Evaluation Metric](#evaluation-metric)

## Datasets

**TODO: add a table of datasets here**

| Datasets        | Video  | Length | Latest Start Times | Download|
| ------------- |:-------------:| -----:| -----:| -----:|
| seq1   | youtube | 100.0 | 10.0 s |link|
| ... | ...  | ... |...| ...|


## Submission Format
Each participant should submit the estimated trajectories for the above datasets and a report describing the adopted method.

### Estimated Trajectories
The estimated trajectories should be stored in plain text files in the following format:

    # timestamp tx ty tz qx qy qz qw
    1.403636580013555527e+09 0 0 0 0 0 0 0
    …… 

The file names should be the same as the names of the bag. For example, the result for “seq1.bag” should be saved as “seq1.txt”. The file should be space separated. Each line stands for the pose at the specified timestamp. The timestamps are in the unit of second and used to establish temporal correspondences with the groundtruth. The first pose should be **no later** than the starting times specified above, and only poses after the starting times will be used for evaluation.

The pose is composed of translation (`tx` `ty` `tz`, in meters) and quaternion (in Hamilton quaternion, the `w` component is at the end). The pose should specify the pose of the IMU in the world frame. For example, after converting the pose to a transformation matrix `Twi`, one should be able to transform the homogeneous point coordinates in IMU frame to world frame as `pw = Twi * pi`.


### Report
In addition to the estimated trajectories, the participants are required to submit a short report (maximum **4** pages) summarizing their approach.
The reports of all teams will be published on the website after the competition.
The format of the report is left to the discretion of the participants, however the report must specify the following information:
* A brief overview of the approach:
  * Filter or optimization-based (or else)?
  * Is the method causal? (i.e. does not use information from the future to predict the pose at a given time).
  * Is bundle adjustment (BA) used? What type of BA, e.g. full BA or sliding window BA?
  * Is loop closing used?
* Exact sensor modalities used (IMU, stereo or mono, event data?)
* Total processing time for each sequence
* Exact specifications of the hardware used
* Whether the same set of parameters is used throughout all the sequences

The participants are welcome to include further details of their approach, eventual references to a paper describing the approach, or any other additional information.


## Evaluation Metric
The submission will be ranked based on the accuracy. We use the same metric as adopted by [KITTI](http://www.cvlibs.net/datasets/kitti/eval_odometry.php). The average translation error (in percentage) over all possible subsequences of a set of certain lengths will be used for ranking the submitted results.
