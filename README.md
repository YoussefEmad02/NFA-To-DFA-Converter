# CFG to PDA

## Table of Contents
1. [Convert any non-deterministic finite automaton to deterministic finite automaton](#convert-any-non-deterministic-finite-automaton-to-deterministic-finite-automaton)
    - [Introduction](#introduction)
    - [System Requirements](#system-requirements)
    - [Installation Instructions](#installation-instructions)
    - [User Guide](#user-guide)
    - [Developer Documentation](#developer-documentation)

## Table Of Figures 
- Figure 1: NFA File
- Figure 2: NFA and Its DFA

## Convert any non-deterministic finite automaton to deterministic finite automaton

### Introduction
This application is designed to help users convert non-deterministic finite automata into deterministic finite automata. The conversion process is based on the subset construction algorithm which systematically constructs DFA states and transitions from those of the NFA.

### System Requirements
- Java Runtime Environment (JRE): 1.8 or above
- JavaFX Library: Required for the graphical user interface
- IDE (Recommended): IntelliJ IDEA, Eclipse, or NetBeans

### Installation Instructions
1. **Download the Source Code**: Obtain the source code from the Repository.
2. **Import Project**: Open your IDE and import the project. Ensure JavaFX libraries are properly configured.

### User Guide

#### Input NFA Details

![Figure 11: NFA File](figure11.png)

1. In the first line, write the number of states.
2. In the second line, type the start state number like this: `start 0`.
3. Then, type your states and transitions in the format: `location input destination`.
   - Example: `0 0 0`

   | Location | Input | Destination |
   |----------|-------|-------------|
   | ...      | ...   | ...         |

4. After typing your states and transitions, type the final state like this: `final 3`.

#### Convert to DFA
- Run `Main.java` to convert NFA to DFA.

#### The Output
- 2 windows will be opened: the input (NFA) and the output (DFA).

![Figure 12: NFA and Its DFA](screenshots/figure12.png)

### Developer Documentation

#### Converter Package

**State**
- Represents individual states within an automaton, handling transitions that might involve multiple destination states (non-deterministic behavior).
- **Key functionalities:**
  - **State Identification:**
    - `id`: An integer to uniquely identify each state.
  - **Managing Transitions:**
    - `transitions`: A Map where each key is a string representing an input symbol and the associated value is a HashSet of State objects.
  - **Constructor (State(int i)):**
    - Initializes a new state with a given identifier and creates a new empty HashMap for managing transitions.
  - **Transition Management (put(String key, State value)):**
    - Manages the addition of transitions to the state.
  - **String Representation (toString()):**
    - Provides a string representation of the state, useful for debugging and visualization.

**Group**
- Extends `ArrayList<State>` to manage collections of State objects with functionalities specific to groups of states.
- **Key points:**
  - **Unique Identifier:**
    - Each Group instance has a unique identifier (id).
  - **Constructors:**
    - Accepts an integer to set the group's ID.
    - Copies states from another group into the new one along with setting a new ID.
  - **Modified Add Method:**
    - Ensures no duplicate states are added to the group.
  - **Access and Modify ID:**
    - Getter and setter methods for the group's ID.
  - **String Representation:**
    - Provides a string representation of the group, including its ID and the list of states.

**NFA_to_DFA**
- Converts an NFA to a DFA.
- **Key points:**
  - **Initialization and Input Reading:**
    - Reads inputs from a file named "nfa".
  - **NFA Visualization:**
    - Visualizes the NFA using a graphical frame.
  - **DFA Conversion Logic:**
    - Converts NFA to DFA using a mapping to track each unique state of the DFA.
  - **Final States Identification:**
    - Identifies and records final states of the DFA.
  - **Output Generation and Storage:**
    - Generates a string representation of the DFA and saves it to a file named "dfa".
  - **DFA Visualization:**
    - Visualizes the constructed DFA.

**Main**
- Handles reading an NFA configuration from a file and initializes the setup for its conversion to a DFA.
- **Key functionalities:**
  - **Static Variables Initialization:**
    - `start`, `inputSymbols`, `dfa`, `final_states`, and `non_final_states`.
  - **Input Processing (input Method):**
    - Reads the automaton's configuration from a specified file.
  - **Main Execution (main Method):**
    - Serves as the entry point of the application.

#### Graphic Package

**Circle**
- Represents a circle in the graphical representation.
- **Key functionalities:**
  - **Static Constants:**
    - `RADIUS` and `DIAMETER`.
  - **Instance Variables:**
    - `id`, `centre`, `angle`, `finalState`.
  - **Constructor:**
    - Initializes a Circle with an ID and coordinates for its center.
  - **Final State Management:**
    - Methods to mark and check if the circle represents a final state.
  - **String Representation:**
    - Provides a string representation of the circle.

**Point**
- Handles basic 2D point operations.
- **Key functionalities:**
  - **Constructor:**
    - Initializes a Point object with integer coordinates.
  - **Distance Calculation:**
    - Calculates the Euclidean distance between points.
  - **Intermediate Point Calculation:**
    - Calculates a point on the line segment between two points at a specified ratio.
  - **String Representation:**
    - Provides a readable string representation of the point.
  - **Equality Method:**
    - Custom equality check with a small tolerance in coordinates.

**Arrow**
- Represents an arrow in the graphical representation.
- **Key functionalities:**
  - **Static Constant:**
    - `POINTER_SIZE`.
  - **Instance Variables:**
    - `id`, `pts`, `p1`, `p2`, `p3`, `input_symbol`, `string_pos`.
  - **Constructor:**
    - Initializes the Arrow with an ID and an empty list of points.
  - **Methods:**
    - Methods to add points, retrieve points, and provide a detailed string representation.
  - **Equality Methods:**
    - Methods to define equality based on the start and end points of the arrow.

**SelfLoop**
- Represents self-loops in a graphical representation.
- **Key functionalities:**
  - **Data Members:**
    - `id`, `centre`, `radius`, `theta`, `input_symbol`, `string_pos`, `p1`, `p2`, `end`.
  - **Constructor:**
    - Initializes a self-loop with an ID, center point, radius, and angle.
  - **String Representation:**
    - Provides a detailed string representation of the self-loop.

**State**
- Represents states of an automaton in a graph-based structure.
- **Key functionalities:**
  - **Data Members:**
    - `id`, `transitions`.
  - **Constructor:**
    - Initializes a new state with an ID and an empty HashMap for transitions.
  - **Methods:**
    - Methods to add transitions and provide a string representation of the state's ID.

**DataCalculator**
- Processes and calculates data for a graphical representation of an automaton.
- **Key functionalities:**
  - **Data Initialization and Reading:**
    - Methods to read and load automaton data from a file.
  - **Calculations for Graphical Representation:**
    - Methods to calculate positions for states and transitions.
  - **Dimension Handling:**
    - Method to calculate and return the required dimensions for the drawing panel.
  - **Utility Methods for Geometric Calculations:**
    - Methods to calculate rotation of points and positions with respect to other points.
  - **Data Management:**
    - Getter methods to provide access to internal data.
  - **Handling Special Cases:**
    - Handles self-loops and overlapping transitions.

**DrawingPanel**
- Custom JPanel to visualize data processed by DataCalculator.
- **Key functionalities:**
  - **Initialization and Setup:**
    - Constructor initializes the panel with automaton data and sets up event handling.
  - **Event Handling:**
    - Mouse listener to log coordinates on click.
  - **Graphical Rendering:**
    - Overridden `paintComponent` method to render states, self-loops, arrows, and labels.
  - **Utility Functions:**
    - Method to provide color based on element ID.
  - **Debugging and Information Display:**
    - Console outputs for debugging graphical components.

**MainFrame**
- Main window for displaying a graphical representation of an automaton.
- **Key functionalities:**
  - **Constructor:**
    - Initializes the frame with a file and title, sets up event handling, and adds DrawingPanel.
  - **Main Method:**
    - Entry point of the application.
