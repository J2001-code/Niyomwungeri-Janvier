# Niyomwungeri-Janvier
## Oriented Object project
```sql
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
