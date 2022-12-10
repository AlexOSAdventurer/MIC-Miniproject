# PetriNet Design Studio
## PetriNet Overview
PetriNets are a mathematical modeling language for describing distributed systems.
It consists of a set of places that each contain a 'marking' or 'token' variable greater than or equal to 0.
These are connected to a set of transitions, which are 'active' if all places that connect to it, treating it as a destination ('inplaces'), have one or more tokens.
When an active transition is activated, it decrements all 'inplace' counts and increments all 'outplace' counts (places that are connected intuitively treating the transition as a source).
## Applications of PetriNets
They are used in a variety of analyses regarding distributed systems to model such systems in a roughly simplified fashion:
- Chemical reactions
- Biological systems
- Computer and Cyber-Physical systems

Transitions being able to fire at any time, combined with the token counter for each place, provides a minimum viable capacity for modeling the above systems.
Examples of these are included within the 'seeds' folder and the default docker container database to help get you started.
## Installation of Design Studio
There are two ways in which you can install this design studio:
- Use this docker container directly as a fully containerized prepackaged version of this design studio.
- Install the visualizer and base project seed into your own pre-existing webgme setup manually.

### Using the Design Studio docker container
Follow these steps:
- `docker-compose up -d`. This should build the container but may take up to 10 minutes to finish.
- Wait an additional 30 seconds after the container has built to allow the mongo subcontainer to fully launch - this often crashes the webgme subcontainer.
- Execute `docker-compose up -d` again. You should now have `localhost:8888` available that allows you to use the design studio.

### Installing the Visualizer plugin to your pre-existing webgme installation manually
Follow these steps within your own webgme installation:
- `npm run webgme import viz PetriNetVisualizer AlexOSAdventurer/MIC-Miniproject`

## How to begin modeling once in the studio
Assuming you have the project seeds imported and the visualizer installed, you can create new projects by using the PetriNetBaseModel seed under the seeds folder.
From there you can add places, transitions, and "arcs" (the connections between places and transitions) to the empty network. Arcs are implemented as standard WebGME connections
Keep in mind that there are two arc types: ArcToTransition, and ArcToPlace. These respectively have source types of Place and Transition - Places and Transitions cannot connect to their own type. To create these connections, use the standard pointer creation controls.
Under the marking attribute for places you can change the starting number for each place. This is visually annotated by suffixing all place names with the marking count, and by adding visual circles, each corresponding to a marking count, to the inside of the circle (up until 12, at which it defaults to a textual count).

## Studio Visualizer - Features and How to Use it
You will see a new PetriNetVisualizer available as a potential visualizer for Petri networks. This lets you execute an interaction simulation of the Petri network.
In this simulation, the following features are available to you:
- Triggering an active transition by double clicking it. Transitions are marked active with the color green, inactive with the color red. All place counts and transition activeness should adjust automatically.
- Resetting the simulation back to the starting place-marker state. You can do this with the rest simulation button in the toolbar that has the bottom-right pointing diagonal arrow icon.
- Checking the type of PetriNet, amongst Free Choice Net, Workflow net, state machine, and marked graph, that the network is. It can be multiple types at once, or none at all (an empty text). This can be done with the "Update Net Type Annotation" button, with the pen on the line icon, in the toolbar. When clicked, the visualizer header display will update with the determined network types;.
- Automatically seeing whether the network is in deadlock (no active transitions) or not - this is annotated next to the network type, and automatically changes as you activate transitions.
