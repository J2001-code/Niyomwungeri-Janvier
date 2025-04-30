# Niyomwungeri-Janvier
## Oriented Object project
# 🛰️ Mission Management System (Java OOP Project)

This project is a console-based **Mission Management System** implemented using Java and Object-Oriented Programming principles. It simulates organizing missions, assigning personnel, tracking status, and managing mission-specific logic.

---

## 🔧 Features

- Abstract `Mission` class with subclasses (e.g., `RescueMission`, `ExplorationMission`)
- `Personnel` class for handling staff involved in missions
- Assigning personnel to missions with validation
- Mission progress tracking and completion
- Console-based interaction and simulation

---

## 💡 Concepts Used

- Abstraction and inheritance
- Encapsulation of mission logic
- Polymorphism with overridden mission behavior
- Object composition (mission ↔ personnel)

---

## 🛠 Technologies

- Java
- Collections API
- Exception handling
- Console I/O

---

## 🏃‍♂️ How to Run

1. Clone the repo and open in IntelliJ IDEA or any Java IDE
2. Compile and run `Main.java`
3. Use the console interface to add missions, assign personnel, and update progress

---

## ✍️ Author

Part of a series of Java OOP practice projects.


```java
package Question1;

import java.util.List;

public class CombatMission extends Mission {

    public CombatMission(String missionId, String missionName, java.util.Date startDate, java.util.Date endDate, List<Personnel> assignedPersonnel) {
        super(missionId, missionName, startDate, endDate, assignedPersonnel);
    }

    @Override
    public void assignTask() {
        if (assignedPersonnel.size() < 3) {
            System.out.println("CombatMission requires at least 3 personnel.");
            return;
        }
        for (Personnel p : assignedPersonnel) {
            System.out.println("Assigning combat task to " + p.getPersonnelName());
        }
    }

    @Override
    public void allocateResources(List<Resource> availableResources) {
        boolean allocated = false;
        for (Resource r : availableResources) {
            if (r.getResourceName().equalsIgnoreCase("Ammunition") && r.getQuantity() > 0) {
                System.out.println("Ammunition allocated for Combat Mission.");
                r.setQuantity(r.getQuantity() - 1);
                allocated = true;
            }
        }
        if (!allocated) {
            System.out.println("No Ammunition available for Combat Mission!");
        }
    }

    @Override
    public void trackMissionProgress() {
        System.out.println("Tracking combat operations...");
        this.status = "IN_PROGRESS";
    }

    @Override
    public void generateMissionReport() {
        System.out.println("--- Combat Mission Report ---");
        System.out.println("Mission: " + missionName + " | Status: " + status);
    }
}

```
