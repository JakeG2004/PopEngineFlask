# Population Engine
Written with Python using Flask. This software simulates microbe populations and interactions using the [Lotka-Volterra](https://math.libretexts.org/Bookshelves/Applied_Mathematics/Mathematical_Biology_(Chasnov)/01%3A_Population_Dynamics/1.04%3A_The_Lotka-Volterra_Predator-Prey_Model)
model using discrete time steps.

## Install
Ensure that you have python3, matplotlib, numpy, tkinter, and flask installed

Install [Python](https://www.python.org/downloads/), then
```
pip3 install matplotlib
pip3 install numpy
pip3 install flask
```

## Run
Once all of the requisite software is intalled, run the app with:
```
flask run
```

At this point, your command line should give you an IP to connect to the website with. It should look something like this:
```
 * Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on http://127.0.0.1:5000
Press CTRL+C to quit
```

## Usage
Once getting your Flask website up and running, it should resemble this:
![Screenshot from 2025-05-20 16-25-24](https://github.com/user-attachments/assets/2ce50c71-8b48-445c-a0e5-174890e62110)

### The Graphs
The simulator has three graphs. From left to right they are
1) Microbial Growth Over Time
  * Plots the populations of the microbes at each time step and connects with a line
2) Carry Capacity Over Time
  * Plots the carrying capacities of each of the microbes at each time step and connects with a line
3) Resource Levels Over Time
  * Shows the amounts of each resource at each time step and connects with a line

## Time Controls
The `Next Time Step` and `Fast Forward` options allow you to advance the simulation.
* `Next Time Step` advances the simulation by one time step
* `Fast Forward` allows you to enter a natural (integers from 1 - n) number of steps to advance the simulation

## Environment Options
![Screenshot from 2025-05-20 16-59-37](https://github.com/user-attachments/assets/318ddec1-ba64-46f8-8d8d-c2ffd79d0c83)

The environment options page has two buttons, `Add Resource` and `Edit Environment`

### Add Resource
![Screenshot from 2025-05-20 16-59-00](https://github.com/user-attachments/assets/333887d8-b13b-423b-aadb-ce5a39fcce4e)

The `Add Resource` page allows you to add a new resource to the environment and give it a name

### Edit Environment
![Screenshot from 2025-05-20 16-31-36](https://github.com/user-attachments/assets/45c8c1a7-46ab-4e3c-be42-53ab0629e352)

The `Edit Environment` page allows you to edit the resources in the simulated environment. Each resource has two properties which can be modified here.
1) `Current Amount`
  * The Current amount of the given resource present in the environment
2) `Current Refresh Rate`
  * The amount of this resource which is added at each time step.
    
**NOTE**: If you do not have any resources, nothing will appear on this page.

## Microbe Options
![Screenshot from 2025-05-20 16-59-59](https://github.com/user-attachments/assets/ce82d2fe-bc13-4da6-b338-bcca0dc2cf3e)

The microbe options page has 3 buttons, `Add Microbe`, `Edit Microbe`, and `Delete Microbe`.

### Add Microbe
![Screenshot from 2025-05-20 16-40-50](https://github.com/user-attachments/assets/b99bff3a-e658-4086-85d1-109f4aa33f5b)

#### General Information
The `microbe name`, and `initial population` should be fairly simple. The `growth rate` is a decimal number > 0 which indicates how fast a species grows. 1 is the standard.

#### Required Resources
For each resource, specify how much of that resource per time step is needed for a single microbe in the population to survive. Empty entries are assumed to be 0.

#### Produced Resources
For each resource, specify how much of that resource per time step is produced by a single microbe in the population. Empty entries are assumed to be 0.

#### Toxins
Toxins work by impacting the efficiency of a given microbe. A highly toxic resource may cut efficiency down to 20 or 30%.

To enable toxicity for a given resource, check its checkbox. It will have the following fields
1) **Toxicity Level**
  * How dangerous / toxic this resource is to a microbe. 0.1 is not very toxic, 10 is very toxic.
2) **Minimum Safe Toxicity**(0-1)
  * The minimum density of this resource that the microbe needs to operate at maximum efficiency.
  * If 0, then the microbe will operate at full efficiency until its maximum safe toxicity.
  * If 1, then the microbe will never operate at full efficiency unless the resource is not present
3) **Maximum Safe Toxicity** (0-1)
  * The maximum density of this resource that the microbe will operate at maximum efficiency at
  * If 0, then the microbe will never operate at full efficiency unless the resource is not present
  * If 1, then the microbe will always operate at full efficiency beyond its minimum safe density
4) **Lethal Toxicity** (0-1)
  * The density of this resource in the environment that will immediately kill the microbe
  * If 0, then the microbes will always die
  * If .5, then the microbes will die if this resource exceeds 50% of the total resources in the environment
  * If 1, then the microbes will only die if the environment is 100% this resource.

**NOTE**: Density is calculated as the number of this element in the environment divided by the total number of elements in the environment. AKA, the percentage of this resource in the environment.

### Edit Microbe
![Screenshot from 2025-05-20 16-55-50](https://github.com/user-attachments/assets/a2ef2b69-9d75-464f-b142-f240e0cbb875)

This page allows you to edit the populations of the microbes that you have. Additionally, you can view the numbers that were defined during Microbe creation.

### Delete Microbes
![Screenshot from 2025-05-20 16-57-49](https://github.com/user-attachments/assets/25558509-0ade-4a1f-b554-37059e0c2a8f)

This page allows you to delete microbes from the simulation. Note that they will be removed from the graph.


## Presets
![Screenshot from 2025-05-20 16-58-27](https://github.com/user-attachments/assets/009abf44-b28c-4c16-9593-c1617fe71e15)

The simulator has 3 presets. Click on one to use it as your environment.
1) 2 Microbe symbiosis
  * A healthy relationship between two microbes which cycle resources
2) 2 Microbes with Lead
  * Meant to demonstrate Toxicity.
  * Same as the first simulation, except Lead is slowly being added to the environment and will eventually kill the microbes.
3) 3 Microbe symbiosis
  * Same as above, except there is a third microbe which is responsible for keeping lead at a manageable level.

## Reset
Press this button to entirely reset all microbes and environmental settings.
