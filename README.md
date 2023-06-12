# WORK IN PROGRESS
# **"Trigger" Script for Trigger Volumes in Unity**

The "Trigger" script is an abstract class used to create trigger volumes in Unity. It is instantiated with a MeshFilter and a MeshRenderer, allowing you to define specific areas in the game space that react to interactions from other objects.

The "Trigger" script includes the following features:

- It allows specifying a material for the trigger volume rendering.

- It handles events triggered when an object enters, stays, or exits the trigger volume.

- It supports a cooldown for triggering (useful for triggers that should not be activated too frequently).

- It provides the option to disable the GameObject after the trigger is activated.

- It allows specifying the layers the trigger can interact with

.

To use the "Trigger" script, you need to create a derived class and implement the following abstract methods:

- **`Init()`**: Initialization of the trigger.

- **`TriggerEnter(Collider other)`**: Actions to perform when the volume is activated by an entering object.

- **`TriggerExit(Collider other)`**: Actions to perform when the volume is activated by an exiting object.

- **`TriggerStay(Collider other)`**: Actions to perform when the volume is activated by an object staying inside.

# **"TriggerBox" Script**

The "TriggerBox" script is a derived class of the "Trigger" script that allows creating box-shaped trigger volumes in Unity. It adds specific functionalities for boxes, such as a BoxCollider component and a quick creation option from the editor.

## **Required Components**

The "TriggerBox" script requires the following components on the GameObject:

- BoxCollider: Defines the trigger area as a box.

The "TriggerBox" script extends the "Trigger" script by adding the **`Init()`** method, which configures the GameObject's mesh to match a cube. Additionally, it uses a preprocessor directive **`#if UNITY_EDITOR`** to add a context menu in the editor for quickly creating box-shaped trigger volumes.

When selecting the "GameObject/Trigger/Trigger Box" option from the editor menu, a trigger box will be created with a BoxCollider component, and the "TriggerBox" script will be automatically attached.

# **"TriggerUse" Script for User Input-based Trigger Volumes in Unity**

The "TriggerUse" script is a derived class of the "Trigger" script that allows creating trigger volumes based on specific user input in Unity. This script adds functionalities related to user input, such as checking for a specific input and the ability to trigger the event only once.

## **Properties**

The "TriggerUse" script contains the following properties:

- **`inputToTrigger`**: A scriptable object of type **`InputButtonScriptableObject`** that represents the user input to check.

- **`triggerOnce`**: A boolean indicating whether the trigger should be disabled after being used.

The "TriggerUse" script extends the "Trigger" script by adding the **`TriggerEnter`** method, which listens for changes in the value of the user input specified in **`inputToTrigger`**. When the value of the user input becomes true, the **`EventOnTriggerInput`** event is triggered.

If the **`triggerOnce`** property is set to true, the script will deactivate after being used once.