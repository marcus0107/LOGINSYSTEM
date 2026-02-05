import java.io.Console;
import java.util.Scanner;

public class LoginSystem {

    public static void main(String[] args) {

        // Correct login credentials
        String correctUsername = "admin";
        String correctPassword = "1234";

        Scanner scanner = new Scanner(System.in);
        Console console = System.console(); // Used to hide password

        int attempts = 3; // User has 3 tries

        while(attempts > 0) {

            System.out.print("Enter Username: ");
            String username = scanner.nextLine();

            String password;

            // If console is available, mask password
            if(console != null){
                char[] passArray = console.readPassword("Enter Password: ");
                password = new String(passArray);
            }
            else{
                // fallback if console not supported (e.g., some IDEs)
                System.out.print("Enter Password: ");
                password = scanner.nextLine();
            }

            // Validate login
            if(username.equals(correctUsername) && password.equals(correctPassword)){
                System.out.println("Login Successful!");
                return;
            }
            else{
                attempts--;
                System.out.println("Incorrect credentials. Attempts left: " + attempts);
            }
        }

        System.out.println("Account locked. Too many failed attempts.");
        scanner.close();
    }
}
