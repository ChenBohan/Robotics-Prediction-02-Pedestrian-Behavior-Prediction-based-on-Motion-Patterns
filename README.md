# Robotics-Prediction-02-Pedestrian-Behavior-Prediction-based-on-Motion-Patterns
Paper: 'Pedestrian Behavior Prediction based on Motion Patt erns for Vehicle-to-Pedestrian Collision Avoidance'
& 'Improved Multi-Level Pedestrian Behavior Prediction Based on Matching with Classified Motion Patterns'

# Pedestrian Behavior Prediction based on Motion Patt erns for Vehicle-to-Pedestrian Collision Avoidance

## Abstract

This paper proposes a prediction method for vehicle-to-pedestrian collision avoidance, which **learns** and then **predicts** pedestrian behaviors as their **motion instances** are being observed. 

During learning, known trajectories are clustered to form Motion Patterns (MP), which become knowledge a priori to a
multi-level prediction model that predicts long-term or short-term pedestrian behaviors.

## Related Works

- Conventionally, pedestrian behavior refers to pedestrian motion in the next time-step [3-8]. Techniques such as neural network [3], Markov models [4], Kalman filter [5, 6], and collision/velocity cones [7, 8] use current and historical motion data as their basis to predict motion in the next time step, which is **short term and restrictive** because they treat the CA problem **locally and sub-optimally** [9].

- In order to perform CA more effectively, some researchers have recently attempted **long-term behavior prediction** for global CA [10, 11]. They predict over a number of future time-steps giving the vehicle a better chance of **making the right action decision**. Clearly, long-term behavior prediction is superior for avoiding collisions with globally optimal paths, but is naturally far more challenging.

- In [10], it treats the **final destination point** of the pedestrian’s movement as a long-term prediction goal, though this does not guarantee collision-free motion because there are many possible routes and motion patterns between each origin-destination pair.

- In [11], long-term prediction is made based on a set of trajectories between a number of **resting places** where people stop and stay. It requires the locations of these resting places be known a priori for the formation of Motion Patterns (MP) of the pedestrian.

## In this paper

- We propose a new prediction method that learns and predicts pedestrian behaviors as their motion
instances are being observed. 
  - The observed trajectories (in terms of spatial location, velocity or heading angle) are clustered using the CGC algorithm [13] to form MP. For each clustered MP, it is evaluated for completeness against a criterion. 
    - They are then classified as **complete MP (MP-C)**, which represents pattern that does not change much over time, 
    - or as **incomplete MP (MP-I)**, which may be updated after subsequent prediction. 
- Based on these MP, a multi-level prediction model is proposed. 
  - It consists of three levels of prediction in which 
    - the **high and middle levels** are both long-term predictions based on the MP-C and MP-I that predict future trajectories over a number of time-steps. 
    - The **low level** uses an AR model [14] to predict future trajectories over the next time step.

## PROPOSED METHOD

### Overview

<img src="https://github.com/ChenBohan/Robotics-Prediction-02-Pedestrian-Behavior-Prediction-based-on-Motion-Patterns/blob/master/Readme_img/overview.png" width = "40%" height = "40%" div align=center />

- To start with, when a group of pedestrian instances at time t are observed, they are first associated with existing trajectories that have been assembled through the previous t-1 time steps.
  -  The association relies on the t-1 instances to optimize a global shortest distance for all instances.
  -  From the newly formed trajectories with spatial location feature, we can derive the corresponding velocity and heading angle features.
- Given the trajectories, MP are clustered using an instance-based clustering algorithm as a general representation of a sub-group of trajectories.
  - Each clustered MP is further classified into MP-C or MP-I which is conditioned upon that the MP has been obtained based on a relative number of observable motion instances.
- Finally, pedestrian behavior prediction accepts three inputs: (1) MP-C; (2) MP-I; and (3) current trajectories.
  
### MP Clustering

To cluster MP from trajectories of one of the three feature dimensions, we employ the constrained gravitational clustering (CGC) method as described in [13].

Analogy to gravitational force, existing clusters separated by a short distance are more likely to form a new cluster compared with those separated by a long distance.

<img src="https://github.com/ChenBohan/Robotics-Prediction-02-Pedestrian-Behavior-Prediction-based-on-Motion-Patterns/blob/master/Readme_img/cluster.png" width = "50%" height = "50%" div align=center />

### MP Classification 

To classify MP, we propose a criterion based on the triangle algorithm [15].

<img src="https://github.com/ChenBohan/Robotics-Prediction-02-Pedestrian-Behavior-Prediction-based-on-Motion-Patterns/blob/master/Readme_img/MP%20Classification.png" width = "50%" height = "50%" div align=center />

## Result

<img src="https://github.com/ChenBohan/Robotics-Prediction-02-Pedestrian-Behavior-Prediction-based-on-Motion-Patterns/blob/master/Readme_img/Multi-level%20prediction%20results.png" width = "50%" height = "50%" div align=center />

<img src="https://github.com/ChenBohan/Robotics-Prediction-02-Pedestrian-Behavior-Prediction-based-on-Motion-Patterns/blob/master/Readme_img/Application.png" width = "50%" height = "50%" div align=center />

# Improved Multi-Level Pedestrian Behavior Prediction Based on Matching with Classified Motion Patterns

## Abstract

- The improvement mainly focuses on the similarity matching criteria between the trajectory and the
clustered MP whose main advantages are that 
  - (1) a reasonable similarity range of MP is automatically calculated instead ofmanually set; 
  - (2) the distance feature and the changing angle feature are considered together for similarity matching while only the distance feature is considered before.
  
<img src="https://github.com/ChenBohan/Robotics-Prediction-02-Pedestrian-Behavior-Prediction-based-on-Motion-Patterns/blob/master/Readme_img/Overview2.png" width = "50%" height = "50%" div align=center />
  
<img src="https://github.com/ChenBohan/Robotics-Prediction-02-Pedestrian-Behavior-Prediction-based-on-Motion-Patterns/blob/master/Readme_img/General%20Algorithmic%20Flow.png" width = "50%" height = "50%" div align=center />  

## Matching

- The matching process in the improved method consists of two stages: 
  - pre-requisite matching
    - In pre-requisite matching, a criterion based on distance between the current trajectory and the MP_C is proposed for deciding whether the current trajectory falls into a reasonable similarity range of the MP_C. 
    - In our previous method, this criterion depends on a manually setting parameter that defines a similarity range of the MP_C. 
    - It is improved that the similarity range of the MP_C can be automatically generated based on the left boundary and the right boundary of the MP_C.
  - similarity matching. 
    - On the other hand, our previous method only considers the distance between the current trajectory and the MP_C when measuring their similarity. 
      - However, there are cases that the current trajectory may not be very similar to the MP_C although they are close to each other.       - In the improved method, we proposed a new similarity matching stage which is performed based on a criterion that considers changing angle calculation and comparison. 
      
<img src="https://github.com/ChenBohan/Robotics-Prediction-02-Pedestrian-Behavior-Prediction-based-on-Motion-Patterns/blob/master/Readme_img/Dimension%20equalization.png" width = "50%" height = "50%" div align=center />
