# ElderCare Home Assistant Ontology

## Project Overview
This ontology models a smart home system designed for elderly care. It represents rooms, devices, activities, and their relationships, enabling reasoning about safety, wellness, and automation using SWRL rules. The goal is to support independent living for older adults while maintaining safety, comfort, and autonomy.

---

## Classes

- **Room**: Represents different rooms in the house.
  - Subclasses: 
    - **Bedroom**
    - **Bathroom**
    - **Kitchen**
    - **LivingRoom**
- **Device**: Smart devices installed in the home.
  - Subclasses:
    - **SmartLight**
    - **MotionSensor**
    - **FallDetector**
    - **Thermostat**
- **Activity**: Actions performed by individuals in the home.
  - Subclasses:
    - **Walking**
    - **Sleeping**
    - **Eating**
    - **TakingMedication**

---

## Object Properties

- **contains**: Links a Room to the Devices it contains.
- **performsActivityIn**: Links an Activity to the Room where it occurs.
- **monitors**: Links a Device to the Activity it monitors.
- **alertsFor**: Links a Device to the Activity it triggers an alert for.

---

## Data Properties

- **hasOccupancy** (Room -> integer): Indicates the number of people present in a room.
- **hasLightLevel** (Room -> float): Represents the lighting level in a room.
- **hasAlertStatus** (Device -> boolean): Indicates whether a device’s alert is active.
- **hasTemperature** (Device -> float): Represents the temperature detected by a device.

---

## Individuals

### Rooms
- **Bedroom1**
- **LivingRoom1**

### Devices
- **SmartLight1** (located in LivingRoom1, initial `hasAlertStatus=true`)
- **MotionSensor1** (located in LivingRoom1)
- **FallDetector1** (located in Bedroom1)

### Activities
- **WalkingActivity1** (performed in LivingRoom1)
- **SleepingActivity1** (performed in Bedroom1)
- **MedicationActivity1**

---

## SWRL Rules

1. **FallDetectorDuringSleeping**  
   Activates the fall detector alert if a sleeping activity occurs in the bedroom.

2. **FallDetectorWalkingAlert**  
   Activates the fall detector alert when a walking activity occurs in any room.

3. **SafeMovementLight**  
   Turns on the smart light (sets `hasAlertStatus=true`) when motion is detected in an occupied room.

4. **ResetLightIfRoomEmpty**  
   Turns off the smart light (sets `hasAlertStatus=false`) if the room is unoccupied.

---

## Reasoner

- **HermiT** or **Pellet** can be used to:
  - Infer device alert statuses.
  - Determine room occupancy effects.
  - Automatically trigger lights or fall detector alerts based on activity and occupancy.
- Ensure that reasoning is active after loading the ontology to see SWRL rules applied.

---

## How to Use

1. Open `ElderCareHome.owl` ontology in Protégé.
2. Go to the **Reasoner** menu and activate HermiT or Pellet.
3. Navigate to the **Individuals** tab to observe inferred alert statuses and relationships.
4. Test the system by changing occupancy, activity instances, or device states and re-running the reasoner.

## Authors
- AGUENAROUS Mohamed
