# The FPV Drone Racing VIO Competition

<p align="center">
  <img width="50%" src="http://rpg.ifi.uzh.ch/datasets/uzh-fpv/trajs/indoor_forward_3_snapdragon_with_gt.gif" alt="The FPV Drone Racing VIO Competition" class="center"> 
</p>

## Description

The participants are required to run their VIO algorithms on sequences selected from the public [UZH-FPV Drone Racing Dataset](http://rpg.ifi.uzh.ch/uzh-fpv.html), which include images, IMU measurements, and event-based camera data recorded with a FPV drone racing quadrotor flown aggressively by an expert pilot. The goal is to estimate the quadrotor motion as accurately as possible, utilizing any desired sensor combinations. The winner will be selected based on the accuracy of the estimated trajectories (details follow below) and will be awarded **1,000 USD** and will also be **invited to present his approach at the [IROS 2019 Workshop "Challenges in Vision-based Drone Navigation"](https://wp.nyu.edu/workshopiros2019mav/)** taking place on November 8, 2019 in Macau.

## Deadline

The **deadline to submit the estimated trajectories and report is Sunday, September 1, 2019. Follow [this link](https://form.jotformeu.com/91574387123360) to submit**.

1. [Datasets](#datasets)
2. [Submission Format](#submission-format)
   * [Estimated Trajectories](#estimated-trajectories)
   * [Report](#report)
3. [Evaluation Metric](#evaluation-metric)
4. [Questions](#questions)

## Datasets ([selected from the UZH FPV Drone Racinf Dataset](http://rpg.ifi.uzh.ch/uzh-fpv.html))

| Datasets        | Video  | Length | Start Time Snapdragon | Start time Davis | Download Snapdragon | Download Davis |
| ------------- |:-------------:| -----:| -----:| -----:| -----:| -----:|
| indoor forward 11   | https://youtu.be/mYKStE7e2aI | 85.68 | 1540824001 s | 1540824001 s | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_forward_11_snapdragon.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_forward_11_snapdragon.zip) | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_forward_11_davis.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_forward_11_davis.zip) |
| indoor forward 12   | https://youtu.be/jNlDgN8fdKA | 124.07 | 1540824296 s | 1540824296 s | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_forward_12_snapdragon.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_forward_12_snapdragon.zip) | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_forward_12_davis.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_forward_12_davis.zip) |
| indoor 45deg 3   | https://youtu.be/q6ELgSAjNMY | 119.82 | 1623 s | 1545305934 s | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_45_3_snapdragon.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_45_3_snapdragon.zip) | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_45_3_davis.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_45_3_davis.zip) |
| indoor 45deg 16   | https://youtu.be/V4OnapxRLD4 | 58.72 | 133 s | 1545315222 s | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_45_16_snapdragon.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_45_16_snapdragon.zip) | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_45_16_davis.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/indoor_45_16_davis.zip) |
| outdoor forward 9   | https://youtu.be/ydaMA4Uta9A  | 314.41 | 372 s | 1540102003 s | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/outdoor_forward_9_snapdragon.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/outdoor_forward_9_snapdragon.zip) | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/outdoor_forward_9_davis.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/outdoor_forward_9_davis.zip) |
| outdoor forward 10  | https://youtu.be/G60gls4qeZ4 | 455.63 | 674 s | 1540102304 s | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/outdoor_forward_10_snapdragon.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/outdoor_forward_10_snapdragon.zip) | [bag](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/outdoor_forward_10_davis.bag), [zip](http://rpg.ifi.uzh.ch/datasets/uzh-fpv/outdoor_forward_10_davis.zip) |

## Submission Format
Each participant should submit the estimated trajectories for the above datasets and a report describing the adopted method. Follow [this link](https://form.jotformeu.com/91574387123360) to submit.

### Estimated Trajectories
The estimated trajectories should be stored in plain text files in the following format:

    # timestamp tx ty tz qx qy qz qw
    1.403636580013555527e+09 0.0 0.0 0.0 0.0 0.0 0.0 0.0
    …… 

The file names should be the same as the names of the bag/zip. For example, the result for “seq1.bag” should be saved as “seq1.txt”. The file should be space separated. Each line stands for the pose at the specified timestamp. The timestamps are in the unit of second and used to establish temporal correspondences with the groundtruth. The first pose should be **no later** than the starting times specified above, and only poses after the starting times will be used for evaluation.

The pose is composed of translation (`tx` `ty` `tz`, in meters) and quaternion (in Hamilton quaternion, the `w` component is at the end). The pose should specify the pose of the IMU in the world frame. For example, after converting the pose to a transformation matrix `Twi`, one should be able to transform the homogeneous point coordinates in IMU frame to world frame as `pw = Twi * pi`.

**Do not publish your trajectory estimates**, as we might re-use some of the datasets for future competitions.

### Report
In addition to the estimated trajectories, the participants are required to submit a short report (maximum **4** pages, 10MB, pdf) summarizing their approach.
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
We will use our publicly available [trajectory evaluation toolbox](https://github.com/uzh-rpg/rpg_trajectory_evaluation) to evaluate the estimated trajectories.

## Questions

If you have a question about the challenge, please file a Github issue in this repository. This way the question and response will be visible to everyone.
Subscribe to [this issue](https://github.com/uzh-rpg/IROS2019-FPV-VIO-Competition/issues/1) to get notified about changes to this document.
