# **Activity Diagrams - Unified Modeling Language (UML)**

An Activity Diagram is a behavioral UML diagram used to represent workflows, processes, and the sequence of activities within a system. It shows how actions are connected and how control flows from one activity to another.

- Illustrates sequential and concurrent activities, along with decision paths and control flow.
- Starts with an initial node and ends with a final node, helping model system behavior over time.

> **Example:** An Online Shopping System activity diagram showing steps such as Browse Products-> Add to Cart -> Make Payment -> Order Confirmation.

## **Uses of Activity Diagram**

Activity diagrams are used to visualize workflows, processes, and the dynamic behavior of a system.

- **Modeling Workflows or Processes:** Represents the sequence of activities in a business process or system workflow.
- **Concurrent or Parallel Processing:** Shows multiple activities that can execute simultaneously.
- **Understanding Dynamic Behavior:** Illustrates how a system behaves and responds to events over time.
- **Clarifying Complex Logic:** Simplifies decision-making and branching processes for better understanding.
- **System Design and Analysis:** Helps analyze, design, and communicate system behavior effectively.
- **Describing Use Cases:** Visualizes the flow of actions and interactions within a use case.

## **Activity Diagram Notations**

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112151723/Activity-Diagram-Notations-660.jpg" alt="Activity-Diagram-Notations" />

### **1. Initial State**

Represents the starting point of an activity or process.

- Shown as a filled black circle in the diagram.
- A process typically has only one initial state unless nested activities are used.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112152513/initial-state-660.jpg" />

> **Example:** Here the initial state of the system before the application is opened.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112152912/Initial-State-symbol-being-used-(1)-660.jpg" />

### **2. Action or Activity State**

Represents the execution of an action or task within a process.

- Shown as a rectangle with rounded corners.
- Represents any action, operation, or event that occurs in the workflow.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112152950/activity-state-660.jpg" />

> **Example**: Consider the previous example of opening an application, opening the application is an activity state in the activity diagram.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112153109/Activity-State-symbol-being-used-660.jpg" alt="Activity-State-symbol-being-used" />

### **3. Action Flow or Control flows**

Represents the transition and sequence of activities within a process.

- Shown as a line with an arrowhead indicating the direction of flow.
- An activity can have multiple incoming and outgoing control flows, with conditions specified on the arrows if required.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112153209/control-flow-660.jpg" alt="control-flow" />

> **Example**: Here both the states transit into one final state using action flow symbols i.e. arrows.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112153322/Using-Action-Flows-for-Transitions-660.jpg" alt="Using-Action-Flows-for-Transitions" />

### **4. Decision node and Branching**

Represents a point where a decision is made to determine the next flow of control.

- Shown with multiple outgoing paths based on conditions or guard expressions.
- Always has two or more outgoing control flow arrows.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112153442/decision-node-660.jpg" alt="Using-Action-Flows-for-Transitions" />

> **Example**: We apply the conditions on input number to display the result :
> - If number is odd then display the number.
> - If number if even then display the error.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112153518/An-Activity-Diagram-using-Decision-Node-660.jpg" alt="An-Activity-Diagram-using-Decision-Node" />

### **5. Guard**


Represents a condition that must be satisfied for a particular flow to be followed.

- Written next to a decision path, often within square brackets.
- Helps control the direction of flow based on specific conditions.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112153635/guard-660.jpg" />

### **6. Fork**

Represents a point where a workflow is split into multiple parallel activities.

- Shown as a solid rectangular bar with one incoming arrow and multiple outgoing arrows.
- Allows several activities to execute simultaneously.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112153718/fork-660.jpg" />

> ***Example:** In the example below, the activity of making coffee can be split into two concurrent activities and hence we use the fork notation.*

### **7. Join**

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112153750/A-Diagram-using-Fork-Notation-660.jpg" />

Represents a point where multiple parallel activities merge into a single flow.

- Shown with two or more incoming edges and one outgoing edge.
- Synchronizes concurrent activities before proceeding to the next step.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112153918/join-660.jpg" />

> ***Example:** When both activities i.e. steaming the milk and adding coffee get completed, we converge them into one final activity.*

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112154002/A-Diagram-using-Join-Notation-660.jpg" />

### **8. Merge or Merge Event**

Represents a point where multiple alternative paths combine into a single flow.

- Merges two or more workflow paths into one outgoing path.
- The process continues regardless of which incoming path was followed.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112154039/merge-660.jpg" />

> **Example:** In the diagram below: we can't have both sides executing concurrently, but they finally merge into one. A number can't be both odd and even at the same time.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112154111/An-Activity-Diagram-using-Merge-Notation-(1)-660.jpg" />

### **9. Swimlanes**

Represents a grouping of activities based on roles, responsibilities, or processes.

- Shown as a rectangular row or column in the activity diagram.
- Helps identify who is responsible for each activity and improves workflow clarity.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112154155/swimlane-660.jpg" />

> **Example:** Here different set of activities are executed based on if the number is odd or even. These activities are grouped into a swimlane.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112154228/An-Activity-Diagram-making-use-of-Swimlanes-660.jpg" />

### **10. Time Event**

Represents an event that pauses the workflow for a specific period of time.

- Shown using an hourglass symbol in the activity diagram.
- Used when an activity or event requires a time delay before continuing.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112154305/time-event-660.jpg" />

> ***Example:** Let us assume that the processing of an image takes a lot of time. Then it can be represented as shown below.*

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112154337/An-Activity-Diagram-using-Time-Event-Notation-660.jpg" alt="An-Activity-Diagram-using-Time-Event-Notation" />

### **11. Final State or End State**

Represents the point where a process or activity reaches completion.

- Shown as a filled circle inside another circle.
- A system or process can have multiple final states.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240112154422/final-state-660.jpg" />

## **Differences between an Activity diagram and a Flowchart**

An activity diagram is very similar to a flowchart. So let us understand if activity diagrams or flowcharts are any different.

### **Flow Chart**

An algorithm is like a set of clear instructions to solve a problem, and a flowchart is a picture that shows those instructions.

- Flowcharts help programmers visualize the steps of an algorithm and plan the logic required to solve a problem before coding.
- They are also used to model business workflows and decision-making processes, making them a simple precursor to activity diagrams.

> ***Example:** A manufacturer uses a flow chart to explain and illustrate how a particular product is manufactured.*
> 

| **Flowchart** | **Activity Diagram** |
| --- | --- |
| Represents the step-by-step flow of a process or algorithm | Represents the flow of activities and actions in a system |
| Used mainly for procedural or algorithmic logic | Used to model workflows and business processes |
| Focuses on control flow using symbols like start, process, decision | Focuses on activities, decisions, parallel flows, and transitions |
| Simple and easy to understand | More expressive and detailed than flowcharts |
| Commonly used in programming and problem-solving | Commonly used in UML for system and process modeling |
| Does not support concurrency well | Supports parallel and concurrent activities |
