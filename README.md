# CarRental1
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Car {
    private String model;
    private boolean available;

    public Car(String model) {
        this.model = model;
        this.available = true;
    }

    public String getModel() {
        return model;
    }

    public boolean isAvailable() {
        return available;
    }

    public void rent() {
        available = false;
    }

    public void returnCar() {
        available = true;
    }
}

class RentalSystem {
    private List<Car> cars;

    public RentalSystem() {
        cars = new ArrayList<>();
        cars.add(new Car("Toyota Camry"));
        cars.add(new Car("Honda Civic"));
        cars.add(new Car("Ford Mustang"));
        // Add more cars
    }

    public void displayAvailableCars() {
        System.out.println("Available Cars:");
        for (Car car : cars) {
            if (car.isAvailable()) {
                System.out.println(car.getModel());
            }
        }
    }

    public boolean rentCar(String model) {
        for (Car car : cars) {
            if (car.getModel().equalsIgnoreCase(model) && car.isAvailable()) {
                car.rent();
                return true;
            }
        }
        return false;
    }

    public boolean returnCar(String model) {
        for (Car car : cars) {
            if (car.getModel().equalsIgnoreCase(model) && !car.isAvailable()) {
                car.returnCar();
                return true;
            }
        }
        return false;
    }
}

public class CarRentalApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        RentalSystem rentalSystem = new RentalSystem();

        while (true) {
            System.out.println("1. Display available cars");
            System.out.println("2. Rent a car");
            System.out.println("3. Return a car");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    rentalSystem.displayAvailableCars();
                    break;
                case 2:
                    System.out.print("Enter the car model you want to rent: ");
                    scanner.nextLine();
                    String rentModel = scanner.nextLine();
                    if (rentalSystem.rentCar(rentModel)) {
                        System.out.println("Car rented successfully.");
                    } else {
                        System.out.println("Car not available for rent.");
                    }
                    break;
                case 3:
                    System.out.print("Enter the car model you want to return: ");
                    scanner.nextLine();
                    String returnModel = scanner.nextLine();
                    if (rentalSystem.returnCar(returnModel)) {
                        System.out.println("Car returned successfully.");
                    } else {
                        System.out.println("Car cannot be returned.");
                    }
                    break;
                case 4:
                    System.out.println("Exiting the application.");
                    scanner.close();
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please choose again.");
            }
        }
    }
}
