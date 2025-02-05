# simple-command-line-application-for-metric-converter
metric converter assignment
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class MetricConverter {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to Metric Converter!\n");
        System.out.println("Please input your query. For example: 1 km = m");
        System.out.println("Enter 'exit' or '-1' to exit the program.\n");

        //this is for the conversions between units
        Map<String, Double> conversions = new HashMap<>();
        conversions.put("km-mile", 0.621371);
        conversions.put("mile-km", 1.60934);
        conversions.put("kg-lb", 2.20462);
        conversions.put("lb-kg", 0.453592);
        conversions.put("g-oz", 0.035274);
        conversions.put("oz-g", 28.3495);
        conversions.put("mm-inch", 0.0393701);
        conversions.put("inch-mm", 25.4);

        while (true) {
            // here is the prompt to tell the user for their input
            System.out.print("Enter your conversion query: ");
            String userInput = scanner.nextLine().trim().toLowerCase();

            if (userInput.equals("exit") || userInput.equals("-1")) {
                System.out.println("Goodbye!");
                break;
            }

            try {
                // Splitting the input into parts
                String[] parts = userInput.split(" ");
                if (parts.length != 4 || !parts[2].equals("=")) {
                    throw new IllegalArgumentException();
                }

                double value = Double.parseDouble(parts[0]);
                String fromUnit = parts[1];
                String toUnit = parts[3];
                String key = fromUnit + "-" + toUnit;

                // Performing the conversion when the input is valid
                if (conversions.containsKey(key)) {
                    double result = value * conversions.get(key);
                    System.out.printf("%.4f %s = %.4f %s%n", value, fromUnit, result, toUnit);
                } else {
                    System.out.println("Conversion not supported. Please try another.");
                }
            } catch (Exception e) {
                System.out.println("Invalid input format. Example: 1 km = mile");
            }
        }
        scanner.close();
    }
}
