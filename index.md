---
title: about
---
# Vision
### Background and Problem
A team at Stryker is working on replicating the work of Dr. David Joseph Tan on 6-DoF pose estimation and temporal tracking with machine learning for machine vision applications in his PhD Thesis, “Learn to Track: From Images to 3D Data”, and one of his more recent publications, “Looking Beyond the Simple Scenarios: Combining Learners and Optimizers in 3D Temporal Tracking”. 

As a part of the temporal tracking process, random forest models compute a 6-DoF movement matrix to estimate a target object's transformation and rotation from frame to frame. Model training data is obtained in a simulated environment by generating depth frames from random transformations and rotations on the 3D CAD data of a target object. 

With the stated implementation, a target object's CAD data is necessary to obtain training data for the random forest models. The problem is, as Dr. Tan states, “When tracking an object in real scenes, there are situations when its 3D model is not at hand, which makes model-based tracking impossible.” 

The IMT department at Stryker is concerned with developing and preparing technologies which don’t yet have a home. In the case of the 3D tracking software, one of their goals is 
“to develop a machine vision toolbox that provides a generic set of capabilities"
While the obtaining a 3D model is not necessarily difficult, there is still an opportunity for investigation into methods which do not require a 3D model. Hence, a proposed method for using online learning to dynamically train and construct random forest models is being researched.

### Brief Description of Solution Being Provided
To investigate general case tracking, Dr. Tan proposes a method to “From one frame to the next, incrementally add new trees to the forest from different object viewpoints”. The proposed online learning method works as follows: 

> Note: This proposal is based on current understanding of the algorithmic process at the time of this writing. The process may be implemented or discovered to work differently at a later date.

The tracking algorithm has to have a ground truth from which it starts. This ground truth is a set of depth data within a 3D box which is obtained from the first RGB-D frame. The centroid of the object is assumed to be at the center of a bounding box, and the initial object transformation is the translation from the camera center to the centroid. The goal being that we don’t define the object’s initial location at the camera, but rather at the center of a geodesic sphere where it is actually located. Using this initial information, the depth data is used to generate and train <em>n</em> trees per parameter for the starting camera view. The method of training <em>n</em> trees per parameter is only used at the initial frame to establish extra stability before new random forests can be learned. After the initial frame, the process of computing transformations and tracking follows the original process described with exception that upon each new iteration, only one tree per parameter is learned. The geodesic sphere is used is used to avoid re-learning trees from similar viewpoints by finding the closest untrained vertex of the sphere from the camera location in the object coordinate system.

### Goal
In contrast to starting from an initialized random forest, the proposed solution deploys 3D online tracking where the trees are adaptively generated from the initial 3D pose through successive frames. The model is learned on the fly. 

# Team
Student(s): Henri Prudhomme

Logistical Advisor: Professor VanderLinden

Expert Advisor(s): Stryker IMT

# Code
N/A (Proprietary)

# Report
## Review of Relevant Design Norms
This project has the potential to affect human life and health and thus raises questions on the reliability of the proposed technology. An online tracking algorithm that uses dynamic computation introduces the problem of limitless input possibilities, and thus potentially unknown behavior. This project will address this issue by considering the trust norm from “Redemption and Responsible Technology” in <em>Shaping a Digital World</em>, Chapter 4 by Professor Schuurman. 

# Resources
### Project 
Proposal: [link](https://github.com/henripru/online_random_forest_decision_tree_generation/blob/gh-pages/proposal_10_22_20.pdf)

Status Report: [link](https://github.com/henripru/online_random_forest_decision_tree_generation/blob/gh-pages/december_report.pdf)

Final Report: [N/A](https://github.com/henripru/online_random_forest_decision_tree_generation/blob/gh-pages/final_report.pdf)

Unofficial Paper: [N/A](https://github.com/henripru/online_random_forest_decision_tree_generation/blob/gh-pages/unofficial_paper.pdf) 

### Source

Papers
- [Learn To Track](http://mediatum.ub.tum.de/doc/1327403/886321.pdf)

- [Looking Beyond the Simple Scenario](https://ieeexplore.ieee.org/document/8007238)

- [Redemption and Responsible Technology](https://digitalcollections.dordt.edu/cgi/viewcontent.cgi?article=2949&context=pro_rege)

Computer Science Website: [Calvin University Department of Computer Science](https://computing.calvin.edu)
