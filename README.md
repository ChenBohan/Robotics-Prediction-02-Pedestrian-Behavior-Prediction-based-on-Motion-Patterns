# Robotics-Prediction-02-Pedestrian-Behavior-Prediction-based-on-Motion-Patterns
Paper: 'Pedestrian Behavior Prediction based on Motion Patt erns for Vehicle-to-Pedestrian Collision Avoidance'
& 'Improved Multi-Level Pedestrian Behavior Prediction Based on Matching with Classified Motion Patterns'

### Pedestrian Behavior Prediction based on Motion Patt erns for Vehicle-to-Pedestrian Collision Avoidance

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



