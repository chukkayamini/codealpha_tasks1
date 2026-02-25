# codealpha_tasks1
import java.util.ArrayList;
import java.util.Scanner;

class Student {
    String name;
    ArrayList<Integer> grades;

  
    Student(String name) {
        this.name = name;
        grades = new ArrayList<>();
    }

 
    void addGrade(int grade) {
        grades.add(grade);
    }
    double getAverage() {
        if (grades.isEmpty()) return 0;
        int sum = 0;
        for (int g : grades) {
            sum += g;
        }
        return (double) sum / grades.size();
    }
    int getHighest() {
        int highest = Integer.MIN_VALUE;
        for (int g : grades) {
            if (g > highest) {
                highest = g;
            }
        }
        return highest;
    }

    int getLowest() {
        int lowest = Integer.MAX_VALUE;
        for (int g : grades) {
            if (g < lowest) {
                lowest = g;
            }
        }
        return lowest;
    }
    void displayReport() {
        System.out.println("\nStudent Name: " + name);
        System.out.println("Grades: " + grades);
        System.out.println("Average: " + getAverage());
        System.out.println("Highest: " + getHighest());
        System.out.println("Lowest: " + getLowest());
    }
}

public class StudentGradeTracker {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ArrayList<Student> students = new ArrayList<>();

        System.out.print("Enter number of students: ");
        int n = sc.nextInt();
        sc.nextLine(); // consume newline

        for (int i = 0; i < n; i++) {
            System.out.print("\nEnter student name: ");
            String name = sc.nextLine();

            Student student = new Student(name);

            System.out.print("Enter number of subjects: ");
            int subjects = sc.nextInt();

            for (int j = 0; j < subjects; j++) {
                System.out.print("Enter grade for subject " + (j + 1) + ": ");
                int grade = sc.nextInt();
                student.addGrade(grade);
            }
            sc.nextLine(); // consume newline
            students.add(student);
        }
        System.out.println("\n===== Student Summary Report =====");
        for (Student s : students) {
            s.displayReport();
        }

        sc.close();
    }
}