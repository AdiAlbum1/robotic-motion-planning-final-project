# Robotic Motion Planning - Final Project

## Table of Contents

- [Task](#task)
- [Installation](#installation)
- [Project Description](#project_description)
- [Training Procedure](#training_procedure)
- [Usage](#usage)

## Task
Sampling based approaches for robotic motion planning suffer from the ability to find a valid path in scenes with critical narrow passageways. My project proposal is a machine-learning based solution recommending a sample point in the scene’s narrow passageway.
A deep neural network which reads as input the image describing the scene: including its source, target and obstacles, and outputs two parameters describing the recommended sample point in the narrow passageway.
To keep the project contained we’ll focus on a single disc robot translating in the plane.

## Installation
```sh
git clone https://github.com/AdiAlbum1/robotic-motion-planning-final-project
cd robotic-motion-planning-final-project
pip install pipenv
pipenv install
pipenv shell
```

## Project Description
- ```python generate_base_obstacle_images.py ``` : Reads as input the JSON files from ```input_json_obstacles/``` contatining the scene's description, and generates binary images of the scene's obstacles
- ``` python train.py``` : Trains a Deep Neural Network for the above regression task
- ``` improved_prm.py``` : Our product. An improved PRM implementation where the first sampled point is given by the CNN

## Training Procedure
### Data
1. Randomly select a base obstacle map with a single critical passageway.
   <br>We manually generated multiple base obstacles maps with single critical passageways using CGAL's scene designer.
   The JSON files describing the scenes were tranformed to images using ```generate_base_obstacle_images.py```
   The generated scenes contain various obstacle maps with horizontal passageways at positions (0,0), (1,0), ..., (8,0)
   as in the following images
    * (0,0):
    <br>![(0,0) - Example](samples/base_(0,0).png)
    * (3,0):
    <br>![(3,0) - Example](samples/base_(3,0).png)

2. Randomly translate the obstacle map along the y-axis
    * A slight translation up along the y-axis
    <br>![(0,0) - Example translated](samples/base_(0,0)\_translated.png)
    * A slight translation down along the y-axis
    <br>![(3,0) - Example translated](samples/base_(3,0)\_translated.png)

3. Randomly rotate the image around its center with {0, 90, 180, 270} degrees
    * A rotation by 90 degrees
    <br>![(0,0) - Example rotated](samples/base_(0,0)\_rotated.png)
    * A rotation by 180 degrees
    <br>![(3,0) - Example rotated](samples/base_(3,0)\_rotated.png)

4. Randomly scattered additional obstacles
    * ![(0,0) - With scattered obstacles](samples/base_(0,0)\_with_obstacles.png)
    * ![(3,0) - With scattered obstacles](samples/base_(3,0)\_with_obstacles.png)

5. Ground truth positions are maintained with above augmentations
    * ![(0,0) - With ground truth](samples/base_(0,0)\_with_obstacles_gt.png)
    * ![(3,0) - With ground truth](samples/base_(3,0)\_with_obstacles_gt.png)

### Model

## Usage
TBD