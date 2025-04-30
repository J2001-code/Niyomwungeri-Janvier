
## Oriented Object projects
#  Mission Management System (Java OOP Project)

This project is a console-based **Mission Management System** implemented using Java and Object-Oriented Programming principles. It simulates organizing missions, assigning personnel, tracking status, and managing mission-specific logic.

---

## Features

- Abstract `Mission` class with subclasses (e.g., `RescueMission`, `ExplorationMission`)
- `Personnel` class for handling staff involved in missions
- Assigning personnel to missions with validation
- Mission progress tracking and completion
- Console-based interaction and simulation

---

## Concepts Used

- Abstraction and inheritance
- Encapsulation of mission logic
- Polymorphism with overridden mission behavior
- Object composition (mission ↔ personnel)

---

##  How to Run

1. Clone the repo and open in IntelliJ IDEA or any Java IDE
2. Compile and run `Main.java`
3. Use the console interface to add missions, assign personnel, and update progress

---
## practice

```java
package Question1;

public class Personnel {
    private String personnelId;
    private String personnelName;
    private String personnelRole;
    private Mission assignedMission;

    public Personnel(String personnelId, String personnelName, String personnelRole) {
        this.personnelId = personnelId;
        this.personnelName = personnelName;
        this.personnelRole = personnelRole;
    }

    // Getters and Setters
    public String getPersonnelId() {
        return personnelId;
    }

    public String getPersonnelName() {
        return personnelName;
    }

    public String getPersonnelRole() {
        return personnelRole;
    }

    public Mission getAssignedMission() {
        return assignedMission;
    }

    public void setAssignedMission(Mission assignedMission) {
        this.assignedMission = assignedMission;
    }
}




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


package Question1;

import java.util.Date;
import java.util.List;

public abstract class Mission {
    protected String missionId;
    protected String missionName;
    protected Date missionStartDate;
    protected Date missionEndDate;
    protected String status;
    protected List<Personnel> assignedPersonnel;

    public Mission(String missionId, String missionName, Date missionStartDate, Date missionEndDate, List<Personnel> assignedPersonnel) {
        this.missionId = missionId;
        this.missionName = missionName;
        this.missionStartDate = missionStartDate;
        this.missionEndDate = missionEndDate;
        this.assignedPersonnel = assignedPersonnel;
        this.status = "PLANNED";
    }

    // Abstract Methods
    public abstract void assignTask();
    public abstract void allocateResources(List<Resource> availableResources);
    public abstract void trackMissionProgress();
    public abstract void generateMissionReport();
}


package Question1;

import java.util.List;

public class ReconMission extends Mission {

    public ReconMission(String missionId, String missionName, java.util.Date startDate, java.util.Date endDate, List<Personnel> assignedPersonnel) {
        super(missionId, missionName, startDate, endDate, assignedPersonnel);
    }

    @Override
    public void assignTask() {
        if (assignedPersonnel.size() < 2) {
            System.out.println("ReconMission requires at least 2 personnel.");
            return;
        }
        for (Personnel p : assignedPersonnel) {
            System.out.println("Assigning reconnaissance task to " + p.getPersonnelName());
        }
    }

    @Override
    public void allocateResources(List<Resource> availableResources) {
        for (Resource r : availableResources) {
            if (r.getResourceName().equalsIgnoreCase("Drone") && r.getQuantity() > 0) {
                System.out.println("Drone allocated for Recon Mission.");
                r.setQuantity(r.getQuantity() - 1);
                return;
            }
        }
        System.out.println("No drone available for Recon Mission!");
    }

    @Override
    public void trackMissionProgress() {
        System.out.println("Tracking reconnaissance progress...");
        this.status = "IN_PROGRESS";
    }

    @Override
    public void generateMissionReport() {
        System.out.println("--- Recon Mission Report ---");
        System.out.println("Mission: " + missionName + " | Status: " + status);
    }
}


package Question1;

import java.util.List;

public class RescueMission extends Mission {

    public RescueMission(String missionId, String missionName, java.util.Date startDate, java.util.Date endDate, List<Personnel> assignedPersonnel) {
        super(missionId, missionName, startDate, endDate, assignedPersonnel);
    }

    @Override
    public void assignTask() {
        boolean hasMedic = false;
        for (Personnel p : assignedPersonnel) {
            if (p.getPersonnelRole().equalsIgnoreCase("Medic")) {
                hasMedic = true;
            }
            System.out.println("Assigning rescue task to " + p.getPersonnelName());
        }
        if (!hasMedic) {
            System.out.println("Error: Rescue Mission must have at least one Medic assigned!");
        }
    }

    @Override
    public void allocateResources(List<Resource> availableResources) {
        boolean allocated = false;
        for (Resource r : availableResources) {
            if (r.getResourceName().equalsIgnoreCase("Ambulance") && r.getQuantity() > 0) {
                System.out.println("Ambulance allocated for Rescue Mission.");
                r.setQuantity(r.getQuantity() - 1);
                allocated = true;
            }
        }
        if (!allocated) {
            System.out.println("No Ambulance available for Rescue Mission!");
        }
    }

    @Override
    public void trackMissionProgress() {
        System.out.println("Tracking rescue progress...");
        this.status = "IN_PROGRESS";
    }

    @Override
    public void generateMissionReport() {
        System.out.println("--- Rescue Mission Report ---");
        System.out.println("Mission: " + missionName + " | Status: " + status);
    }
}


package Question1;

public class Resource {
    private String resourceId;
    private String resourceName;
    private int quantity;
    private String resourceType;

    public Resource(String resourceId, String resourceName, int quantity, String resourceType) {
        this.resourceId = resourceId;
        this.resourceName = resourceName;
        this.quantity = quantity;
        this.resourceType = resourceType;
    }

    // Getters and Setters
    public String getResourceId() {
        return resourceId;
    }

    public String getResourceName() {
        return resourceName;
    }

    public int getQuantity() {
        return quantity;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }

    public String getResourceType() {
        return resourceType;
    }
}


package Question1;

import java.util.List;

public class HumanitarianMission extends Mission {

    public HumanitarianMission(String missionId, String missionName, java.util.Date startDate, java.util.Date endDate, List<Personnel> assignedPersonnel) {
        super(missionId, missionName, startDate, endDate, assignedPersonnel);
    }

    @Override
    public void assignTask() {
        for (Personnel p : assignedPersonnel) {
            System.out.println("Assigning humanitarian task to " + p.getPersonnelName());
        }
    }

    @Override
    public void allocateResources(List<Resource> availableResources) {
        boolean hasFood = false;
        boolean hasMedical = false;
        for (Resource r : availableResources) {
            if (r.getResourceName().equalsIgnoreCase("Food Supply") && r.getQuantity() > 0) {
                hasFood = true;
            }
            if (r.getResourceName().equalsIgnoreCase("Medical Kit") && r.getQuantity() > 0) {
                hasMedical = true;
            }
        }
        if (hasFood && hasMedical) {
            System.out.println("Food and Medical supplies allocated for Humanitarian Mission.");
        } else {
            System.out.println("Essential resources missing for Humanitarian Mission!");
        }
    }

    @Override
    public void trackMissionProgress() {
        System.out.println("Monitoring humanitarian distribution...");
        this.status = "IN_PROGRESS";
    }

    @Override
    public void generateMissionReport() {
        System.out.println("--- Humanitarian Mission Report ---");
        System.out.println("Mission: " + missionName + " | Status: " + status);
    }
}

MAIN CLASS:
package Question1;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) throws ParseException {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");

        // Create Personnel
        Personnel p1 = new Personnel("P001", "Alice", "Medic");
        Personnel p2 = new Personnel("P002", "Bob", "Soldier");
        Personnel p3 = new Personnel("P003", "Charlie", "Scout");

        List<Personnel> personnelList = new ArrayList<>();
        personnelList.add(p1);
        personnelList.add(p2);
        personnelList.add(p3);

        // Create Resources
        List<Resource> resources = new ArrayList<>();
        resources.add(new Resource("R001", "Drone", 2, "Equipment"));
        resources.add(new Resource("R002", "Ambulance", 1, "Vehicle"));
        resources.add(new Resource("R003", "Ammunition", 5, "Weapon"));
        resources.add(new Resource("R004", "Medical Kit", 10, "Medical Supplies"));
        resources.add(new Resource("R005", "Food Supply", 15, "Food"));

        // Create a Mission
        Mission reconMission = new ReconMission("M001", "Recon Alpha", sdf.parse("2025-05-01"), sdf.parse("2025-05-10"), personnelList);

        // Perform Mission Operations
        reconMission.assignTask();
        reconMission.allocateResources(resources);
        reconMission.trackMissionProgress();
        reconMission.generateMissionReport();
    }
}




```
# LAND MANAGEMENT SYSTEM
A Java-based Land Management System built with Object-Oriented Programming concepts. Handles land plot registration, ownership validation, transfers, and property data tracking through structured class design and encapsulation.

# Land Management System (Q2)

This project is a console-based **Land Management System** designed using **Java OOP**. It simulates registering land plots, managing ownership, handling transfers, and validating legal property data.

---

##  Features

- Land plot registration with unique identifiers
- Owner management and transfer of ownership
- Area, location, and zoning info tracking
- Abstract `LandPlot` class with specialized subclasses (e.g., `ResidentialLand`, `CommercialLand`)
- Validation of ownership, duplicate plots, and zoning rules

---

##  Purpose

This project demonstrates real-world modeling using Java OOP — simulating how land-related data can be managed and validated in a software system.

---
### practice
```java
package Question2;

import java.util.Date;

public abstract class Land {
    protected String landId;
    protected String ownerName;
    protected String location;
    protected double sizeInAcres;
    protected Date registrationDate;
    protected String landUseStatus;

    public Land(String landId, String ownerName, String location, double sizeInAcres, Date registrationDate, String landUseStatus) {
        this.landId = landId;
        this.ownerName = ownerName;
        this.location = location;
        this.sizeInAcres = sizeInAcres;
        this.registrationDate = registrationDate;
        this.landUseStatus = landUseStatus;
    }

    public abstract boolean validateOwnership();
    public abstract boolean checkZoningCompliance();
    public abstract double calculateTax();
    public abstract void generateLandReport();

    protected void displayBasicInfo() {
        System.out.println("\nLand ID: " + landId);
        System.out.println("Owner: " + ownerName);
        System.out.println("Location: " + location);
        System.out.println("Size (Acres): " + sizeInAcres);
        System.out.println("Registration Date: " + registrationDate);
        System.out.println("Land Use Status: " + landUseStatus);
    }
}



package Question2;

import java.util.ArrayList;
import java.util.List;

public class LandRegistry {
    private List<Land> lands;

    public LandRegistry() {
        lands = new ArrayList<>();
    }

    public void addLand(Land land) {
        if (land.validateOwnership() && land.checkZoningCompliance()) {
            lands.add(land);
            System.out.println("Land registered successfully!");
        } else {
            System.out.println("Failed to register land. Check ownership or zoning rules.");
        }
    }

    public void displayAllLands() {
        if (lands.isEmpty()) {
            System.out.println("No land registered yet.");
        } else {
            for (Land land : lands) {
                land.generateLandReport();
            }
        }
    }
}


package Question2;

import java.util.Date;

public class AgriculturalLand extends Land {

    public AgriculturalLand(String landId, String ownerName, String location, double sizeInAcres, Date registrationDate, String landUseStatus) {
        super(landId, ownerName, location, sizeInAcres, registrationDate, landUseStatus);
    }

    @Override
    public boolean validateOwnership() {
        return !ownerName.isEmpty() && sizeInAcres >= 1;
    }

    @Override
    public boolean checkZoningCompliance() {
        return true; // Assume agricultural zoning
    }

    @Override
    public double calculateTax() {
        return sizeInAcres * 5000 * 0.01; // 1% tax
    }

    @Override
    public void generateLandReport() {
        displayBasicInfo();
        System.out.println("Land Type: Agricultural Land");
        System.out.println("Tax: $" + calculateTax());
        System.out.println("Zoning Compliance: " + (checkZoningCompliance() ? "Compliant" : "Not Compliant"));
        System.out.println("Ownership Validity: " + (validateOwnership() ? "Valid" : "Invalid"));
    }
}


package Question2;

import java.util.Date;

public class CommercialLand extends Land {

    public CommercialLand(String landId, String ownerName, String location, double sizeInAcres, Date registrationDate, String landUseStatus) {
        super(landId, ownerName, location, sizeInAcres, registrationDate, landUseStatus);
    }

    @Override
    public boolean validateOwnership() {
        return !ownerName.isEmpty();
    }

    @Override
    public boolean checkZoningCompliance() {
        return true; // Assume commercial zoning
    }

    @Override
    public double calculateTax() {
        return sizeInAcres * 10000 * 0.025; // 2.5% tax
    }

    @Override
    public void generateLandReport() {
        displayBasicInfo();
        System.out.println("Land Type: Commercial Land");
        System.out.println("Tax: $" + calculateTax());
        System.out.println("Zoning Compliance: " + (checkZoningCompliance() ? "Compliant" : "Not Compliant"));
        System.out.println("Ownership Validity: " + (validateOwnership() ? "Valid" : "Invalid"));
    }
}


package Question2;

import java.util.Date;

public class IndustrialLand extends Land {

    public IndustrialLand(String landId, String ownerName, String location, double sizeInAcres, Date registrationDate, String landUseStatus) {
        super(landId, ownerName, location, sizeInAcres, registrationDate, landUseStatus);
    }

    @Override
    public boolean validateOwnership() {
        return !ownerName.isEmpty();
    }

    @Override
    public boolean checkZoningCompliance() {
        return true; // Assume environmental clearance
    }

    @Override
    public double calculateTax() {
        return sizeInAcres * 12000 * 0.03; // 3% tax
    }

    @Override
    public void generateLandReport() {
        displayBasicInfo();
        System.out.println("Land Type: Industrial Land");
        System.out.println("Tax: $" + calculateTax());
        System.out.println("Zoning Compliance: " + (checkZoningCompliance() ? "Compliant" : "Not Compliant"));
        System.out.println("Ownership Validity: " + (validateOwnership() ? "Valid" : "Invalid"));
    }
}


package Question2;

import java.util.Date;

public class ResidentialLand extends Land {

    public ResidentialLand(String landId, String ownerName, String location, double sizeInAcres, Date registrationDate, String landUseStatus) {
        super(landId, ownerName, location, sizeInAcres, registrationDate, landUseStatus);
    }

    @Override
    public boolean validateOwnership() {
        return !ownerName.isEmpty();
    }

    @Override
    public boolean checkZoningCompliance() {
        return true; // Assume residential zoning
    }

    @Override
    public double calculateTax() {
        return sizeInAcres * 8000 * 0.015; // 1.5% tax
    }

    @Override
    public void generateLandReport() {
        displayBasicInfo();
        System.out.println("Land Type: Residential Land");
        System.out.println("Tax: $" + calculateTax());
        System.out.println("Zoning Compliance: " + (checkZoningCompliance() ? "Compliant" : "Not Compliant"));
        System.out.println("Ownership Validity: " + (validateOwnership() ? "Valid" : "Invalid"));
    }
}

MAIN CLASS
package Question2;

import java.util.Date;

public class Main {
    public static void main(String[] args) {
        LandRegistry registry = new LandRegistry();

        Land land1 = new AgriculturalLand("AG001", "John Smith", "Farm Zone", 5.0, new Date(), "Vacant");
        Land land2 = new ResidentialLand("RS002", "Anna Johnson", "City Center", 1.5, new Date(), "In Use");
        Land land3 = new CommercialLand("CM003", "Business Corp", "Downtown", 3.0, new Date(), "Under Development");
        Land land4 = new IndustrialLand("IN004", "Factory Ltd", "Industrial Area", 8.0, new Date(), "Vacant");

        registry.addLand(land1);
        registry.addLand(land2);
        registry.addLand(land3);
        registry.addLand(land4);

        System.out.println("\n--- Land Registry Report ---");
        registry.displayAllLands();
    }
}


```
#  Nursery School Management System 
A Java OOP project simulating a nursery school system. Includes class-level handling, student registration, teacher assignments, activities, and progress tracking — all using abstract classes, inheritance, and encapsulation.

This project is a console-based **Nursery School Management System** developed using **Object-Oriented Programming (OOP)** in Java. It helps simulate basic operations of a nursery school such as managing students, teachers, class assignments, and activities.

---

##  Features

- ✅ Abstract class `NurseryClass` with concrete subclasses:
  - `BabyClass` (ages 2–3)
  - `MiddleClass` (ages 3–4)
  - `TopClass` (ages 4–5, with assessments)
-  Teacher class with role validation (e.g., only "Early Childhood Educators" can handle Baby Class)
-  Student class with validation:
  - Age checks based on class type
  - Unique ID enforcement
  - Single class enrollment only
-  Activity tracking (e.g., painting, storytelling)
-  Class report generation including teacher, student count, and activities
-  Interactive console menu using `Scanner`

---

## Practice
```java
package Question3;

import java.util.ArrayList;
import java.util.List;

public abstract class NurseryClass {
    protected String classId;
    protected String className;
    protected int maxCapacity;
    protected Teacher assignedTeacher;
    protected List<Student> students = new ArrayList<>();
    protected List<String> activities = new ArrayList<>();

    public NurseryClass(String classId, String className, int maxCapacity) {
        this.classId = classId;
        this.className = className;
        this.maxCapacity = maxCapacity;
    }

    public void assignTeacher(Teacher teacher) throws Exception {
        this.assignedTeacher = teacher;
        teacher.assignToClass(this);
    }

    public abstract void enrollStudent(Student student) throws Exception;
    public abstract void trackProgress();
    public abstract void conductActivity(String activityName);
    public abstract void generateClassReport();

    public String getClassName() {
        return className;
    }

    public List<Student> getStudents() {
        return students;
    }

    public Teacher getAssignedTeacher() {
        return assignedTeacher;
    }

    public List<String> getActivities() {
        return activities;
    }
}


package Question3;

public class Student {
    private String studentId;
    private String studentName;
    private int age;
    private String guardianName;
    private NurseryClass registeredClass;

    public Student(String studentId, String studentName, int age, String guardianName) {
        this.studentId = studentId;
        this.studentName = studentName;
        this.age = age;
        this.guardianName = guardianName;
    }

    public String getStudentId() {
        return studentId;
    }

    public String getStudentName() {
        return studentName;
    }

    public int getAge() {
        return age;
    }

    public String getGuardianName() {
        return guardianName;
    }

    public NurseryClass getRegisteredClass() {
        return registeredClass;
    }

    public void setRegisteredClass(NurseryClass registeredClass) {
        this.registeredClass = registeredClass;
    }

    @Override
    public String toString() {
        return studentName + " (Age: " + age + ")";
    }
}


package Question3;

public class Teacher {
    private String teacherId;
    private String teacherName;
    private String teacherRole;
    private NurseryClass assignedClass;

    public Teacher(String teacherId, String teacherName, String teacherRole) {
        this.teacherId = teacherId;
        this.teacherName = teacherName;
        this.teacherRole = teacherRole;
    }

    public String getTeacherId() {
        return teacherId;
    }

    public String getTeacherName() {
        return teacherName;
    }

    public String getTeacherRole() {
        return teacherRole;
    }

    public NurseryClass getAssignedClass() {
        return assignedClass;
    }

    public void assignToClass(NurseryClass nurseryClass) {
        this.assignedClass = nurseryClass;
    }

    @Override
    public String toString() {
        return teacherName + " (" + teacherRole + ")";
    }
}


package Question3;

public class BabyClass extends NurseryClass {

    public BabyClass(String classId) {
        super(classId, "Baby Class", 15);
    }

    @Override
    public void enrollStudent(Student student) throws Exception {
        if (student.getAge() < 2 || student.getAge() > 3) {
            throw new Exception("Student age not suitable for Baby Class (2–3 years).");
        }
        if (students.size() >= maxCapacity) {
            throw new Exception("Baby Class is full.");
        }
        for (Student s : students) {
            if (s.getStudentId().equals(student.getStudentId())) {
                throw new Exception("Duplicate student ID.");
            }
        }
        if (student.getRegisteredClass() != null) {
            throw new Exception("Student already enrolled in a class.");
        }

        students.add(student);
        student.setRegisteredClass(this);
    }

    @Override
    public void trackProgress() {
        System.out.println("Tracking motor skills and play-based learning.");
    }

    @Override
    public void conductActivity(String activityName) {
        activities.add(activityName);
        System.out.println("Conducting activity in Baby Class: " + activityName);
    }

    @Override
    public void generateClassReport() {
        System.out.println("\n--- Baby Class Report ---");
        System.out.println("Class Name: " + className);
        System.out.println("Assigned Teacher: " + (assignedTeacher != null ? assignedTeacher : "None"));
        System.out.println("Number of Students: " + students.size());
        System.out.println("Activities Conducted: " + activities);
        trackProgress();
    }

    @Override
    public void assignTeacher(Teacher teacher) throws Exception {
        if (!teacher.getTeacherRole().equals("Early Childhood Educator")) {
            throw new Exception("Only Early Childhood Educators can be assigned to Baby Class.");
        }
        super.assignTeacher(teacher);
    }
}


package Question3;

public class MiddleClass extends NurseryClass {

    public MiddleClass(String classId) {
        super(classId, "Middle Class", 20);
    }

    @Override
    public void enrollStudent(Student student) throws Exception {
        if (student.getAge() < 3 || student.getAge() > 4) {
            throw new Exception("Student age not suitable for Middle Class (3–4 years).");
        }
        if (students.size() >= maxCapacity) {
            throw new Exception("Middle Class is full.");
        }
        for (Student s : students) {
            if (s.getStudentId().equals(student.getStudentId())) {
                throw new Exception("Duplicate student ID.");
            }
        }
        if (student.getRegisteredClass() != null) {
            throw new Exception("Student already enrolled in a class.");
        }

        students.add(student);
        student.setRegisteredClass(this);
    }

    @Override
    public void trackProgress() {
        System.out.println("Tracking language development and basic counting skills.");
    }

    @Override
    public void conductActivity(String activityName) {
        activities.add(activityName);
        System.out.println("Conducting activity in Middle Class: " + activityName);
    }

    @Override
    public void generateClassReport() {
        System.out.println("\n--- Middle Class Report ---");
        System.out.println("Class Name: " + className);
        System.out.println("Assigned Teacher: " + (assignedTeacher != null ? assignedTeacher : "None"));
        System.out.println("Number of Students: " + students.size());
        System.out.println("Activities Conducted: " + activities);
        trackProgress();
    }
}


package Question3;

public class TopClass extends NurseryClass {

    public TopClass(String classId) {
        super(classId, "Top Class", 25);
    }

    @Override
    public void enrollStudent(Student student) throws Exception {
        if (student.getAge() < 4 || student.getAge() > 5) {
            throw new Exception("Student age not suitable for Top Class (4–5 years).");
        }
        if (students.size() >= maxCapacity) {
            throw new Exception("Top Class is full.");
        }
        for (Student s : students) {
            if (s.getStudentId().equals(student.getStudentId())) {
                throw new Exception("Duplicate student ID.");
            }
        }
        if (student.getRegisteredClass() != null) {
            throw new Exception("Student already enrolled in a class.");
        }

        students.add(student);
        student.setRegisteredClass(this);
    }

    @Override
    public void trackProgress() {
        System.out.println("Tracking reading, writing, and arithmetic development. Assessments included.");
    }

    @Override
    public void conductActivity(String activityName) {
        activities.add(activityName);
        System.out.println("Conducting activity in Top Class: " + activityName);
    }

    @Override
    public void generateClassReport() {
        System.out.println("\n--- Top Class Report ---");
        System.out.println("Class Name: " + className);
        System.out.println("Assigned Teacher: " + (assignedTeacher != null ? assignedTeacher : "None"));
        System.out.println("Number of Students: " + students.size());
        System.out.println("Activities Conducted: " + activities);
        trackProgress();
    }
}

MAIN CLASS
import Question3.*;

import java.util.*;

public class Main{
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Initialize classes
        BabyClass babyClass = new BabyClass("BC001");
        MiddleClass middleClass = new MiddleClass("MC001");
        TopClass topClass = new TopClass("TC001");

        Map<String, Teacher> teacherMap = new HashMap<>();
        Map<String, Student> studentMap = new HashMap<>();

        while (true) {
            System.out.println("\n--- Nursery School Management ---");
            System.out.println("1. Add Teacher");
            System.out.println("2. Assign Teacher to Class");
            System.out.println("3. Add Student");
            System.out.println("4. Enroll Student to Class");
            System.out.println("5. Conduct Activity");
            System.out.println("6. Generate Class Report");
            System.out.println("0. Exit");
            System.out.print("Choose an option: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // clear newline

            try {
                switch (choice) {
                    case 1 -> {
                        System.out.print("Teacher ID: ");
                        String id = scanner.nextLine();
                        System.out.print("Name: ");
                        String name = scanner.nextLine();
                        System.out.print("Role: ");
                        String role = scanner.nextLine();
                        Teacher t = new Teacher(id, name, role);
                        teacherMap.put(id, t);
                        System.out.println("Teacher added.");
                    }

                    case 2 -> {
                        System.out.print("Enter Teacher ID: ");
                        String id = scanner.nextLine();
                        Teacher t = teacherMap.get(id);
                        if (t == null) throw new Exception("Teacher not found.");
                        System.out.print("Assign to (baby/middle/top): ");
                        String classType = scanner.nextLine();
                        switch (classType.toLowerCase()) {
                            case "baby" -> babyClass.assignTeacher(t);
                            case "middle" -> middleClass.assignTeacher(t);
                            case "top" -> topClass.assignTeacher(t);
                            default -> throw new Exception("Invalid class type.");
                        }
                        System.out.println("Teacher assigned.");
                    }

                    case 3 -> {
                        System.out.print("Student ID: ");
                        String id = scanner.nextLine();
                        if (studentMap.containsKey(id)) throw new Exception("Duplicate student ID.");
                        System.out.print("Name: ");
                        String name = scanner.nextLine();
                        System.out.print("Age: ");
                        int age = scanner.nextInt(); scanner.nextLine();
                        System.out.print("Guardian Name: ");
                        String guardian = scanner.nextLine();
                        Student s = new Student(id, name, age, guardian);
                        studentMap.put(id, s);
                        System.out.println("Student added.");
                    }

                    case 4 -> {
                        System.out.print("Enter Student ID: ");
                        String id = scanner.nextLine();
                        Student s = studentMap.get(id);
                        if (s == null) throw new Exception("Student not found.");
                        System.out.print("Enroll to (baby/middle/top): ");
                        String classType = scanner.nextLine();
                        switch (classType.toLowerCase()) {
                            case "baby" -> babyClass.enrollStudent(s);
                            case "middle" -> middleClass.enrollStudent(s);
                            case "top" -> topClass.enrollStudent(s);
                            default -> throw new Exception("Invalid class type.");
                        }
                        System.out.println("Student enrolled.");
                    }

                    case 5 -> {
                        System.out.print("Which class (baby/middle/top): ");
                        String classType = scanner.nextLine();
                        System.out.print("Activity name: ");
                        String activity = scanner.nextLine();
                        switch (classType.toLowerCase()) {
                            case "baby" -> babyClass.conductActivity(activity);
                            case "middle" -> middleClass.conductActivity(activity);
                            case "top" -> topClass.conductActivity(activity);
                            default -> throw new Exception("Invalid class type.");
                        }
                    }

                    case 6 -> {
                        System.out.print("Which class report (baby/middle/top): ");
                        String classType = scanner.nextLine();
                        switch (classType.toLowerCase()) {
                            case "baby" -> babyClass.generateClassReport();
                            case "middle" -> middleClass.generateClassReport();
                            case "top" -> topClass.generateClassReport();
                            default -> throw new Exception("Invalid class type.");
                        }
                    }

                    case 0 -> {
                        System.out.println("Exiting system. Goodbye!");
                        scanner.close();
                        return;
                    }

                    default -> System.out.println("Invalid choice.");
                }
            } catch (Exception e) {
                System.out.println("Error: " + e.getMessage());
            }
        }
    }
}

```





