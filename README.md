# codealpha_tasks1
import java.util.ArrayList;
import java.util.Scanner;

class Room {
    int roomNumber;
    String category;
    boolean isBooked;

    Room(int roomNumber, String category) {
        this.roomNumber = roomNumber;
        this.category = category;
        this.isBooked = false;
    }
}

class Reservation {
    String customerName;
    Room room;

    Reservation(String customerName, Room room) {
        this.customerName = customerName;
        this.room = room;
        room.isBooked = true;
    }
}

public class HotelReservationSystem {

    static ArrayList<Room> rooms = new ArrayList<>();
    static ArrayList<Reservation> reservations = new ArrayList<>();

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        initializeRooms();

        int choice;

        do {
            System.out.println("\n===== HOTEL RESERVATION SYSTEM =====");
            System.out.println("1. View Available Rooms");
            System.out.println("2. Book Room");
            System.out.println("3. Cancel Reservation");
            System.out.println("4. View Bookings");
            System.out.println("5. Exit");
            System.out.print("Enter choice: ");
            choice = sc.nextInt();
            sc.nextLine();

            switch (choice) {
                case 1:
                    viewAvailableRooms();
                    break;
                case 2:
                    bookRoom(sc);
                    break;
                case 3:
                    cancelReservation(sc);
                    break;
                case 4:
                    viewBookings();
                    break;
                case 5:
                    System.out.println("Thank you!");
                    break;
                default:
                    System.out.println("Invalid choice!");
            }

        } while (choice != 5);

        sc.close();
    }

    // Initialize sample rooms
    static void initializeRooms() {
        rooms.add(new Room(101, "Standard"));
        rooms.add(new Room(102, "Standard"));
        rooms.add(new Room(201, "Deluxe"));
        rooms.add(new Room(202, "Deluxe"));
        rooms.add(new Room(301, "Suite"));
    }

    static void viewAvailableRooms() {
        System.out.println("\nAvailable Rooms:");
        for (Room room : rooms) {
            if (!room.isBooked) {
                System.out.println("Room No: " + room.roomNumber + " | Category: " + room.category);
            }
        }
    }

    static void bookRoom(Scanner sc) {
        System.out.print("Enter your name: ");
        String name = sc.nextLine();

        System.out.print("Enter room number to book: ");
        int roomNumber = sc.nextInt();

        for (Room room : rooms) {
            if (room.roomNumber == roomNumber && !room.isBooked) {
                Reservation reservation = new Reservation(name, room);
                reservations.add(reservation);
                System.out.println("Room booked successfully!");
                return;
            }
        }

        System.out.println("Room not available!");
    }

    static void cancelReservation(Scanner sc) {
        System.out.print("Enter your name to cancel booking: ");
        String name = sc.nextLine();

        for (Reservation r : reservations) {
            if (r.customerName.equalsIgnoreCase(name)) {
                r.room.isBooked = false;
                reservations.remove(r);
                System.out.println("Reservation cancelled successfully!");
                return;
            }
        }

        System.out.println("Reservation not found!");
    }

    static void viewBookings() {
        System.out.println("\nBooking Details:");
        for (Reservation r : reservations) {
            System.out.println("Customer: " + r.customerName +
                    " | Room No: " + r.room.roomNumber +
                    " | Category: " + r.room.category);
        }
    }
}