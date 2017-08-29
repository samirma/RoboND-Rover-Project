## Project: Search and Sample Return
[//]: # (Image References)
[image1]: warped_example.jpg
[image2]: warped_threshed.jpg
[image3]: autonomous_mode.png

## [Rubric](https://review.udacity.com/#!/rubrics/916/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  
### Notebook Analysis
#### 1. Run the functions provided in the notebook on test images (first with the test data provided, next on data you have recorded). Add/modify functions to allow for color selection of obstacles and rock samples.

In order to find the rocks, it was added a new method called find_rocks.
Below how this method works:
find_rocks receives two parameters an image which we are going to work on and an RGB level. 
First, it uses the given level param to filter the image in order to select all image's pixels that match with that level, then a map with its pixels is created and returned by the method.

Currently, the RGB level used to filter only the yellow rocks is (110, 110, 50)


#### 1. Populate the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Run `process_image()` on your test data using the `moviepy` functions provided to create video output of your result. 

First it was used a perspect transform in a image to remove a rover perspect point of view

![alt text][image1]

It was applied a not evil color threshold and then applied a map in order to find a navagable pixels

![alt text][image2]

And then it was possible to find out the rover coordinates using rover_coords method and then convert it to world coordinates with pix_to_world method.

Now with this rover and world coordinates, it is possible to populate the map

Same approach was used to find whatever is a rock or not in the image and get its coordinate for a navigation and mapping proposes

### Autonomous Navigation and Mapping

#### 1. Fill in the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.

For the perception_step() it was used these main methods with its descriptions:

- perspect_transform: It is used to transform the image from the robot perspective to a ground plane

- color_thresh: Return a navigable ground map based on its color

- rover_coords: It is needed in order to convert all image pixels to a rover coordinates

- pix_to_world: It used to convert rover coordinates into a world coordinates for a world mapping proposes

- to_polar_coords: Convert every coordinate into an angle and distance for a decision_step method

- find_rocks: Return a rock map based on its yellow color a process very similar to the color_thresh method

#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  

It was used a 1280x800 resolution with Fantastic quality in windows mode
Most of the time it got 29 FPS

It was used pretty much the same tecniches used in notebook 

![alt text][image3]

## Future
It was noticed that some times the rover stuck in some rocks, it can be solved with some improvements on the decision_step.
A good approach would find a way to make the rover go to unmapped areas whenever its find itself in an alley
For sure a rock picking should be on the to-do list for the future.
