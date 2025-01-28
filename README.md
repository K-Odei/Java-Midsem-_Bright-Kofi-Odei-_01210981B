import java.util.Scanner;

class ElectricityBill {
    private String consumerNo;
    private String consumerName;
    private int previousMonthReading;
    private int currentMonthReading;
    private String connectionType;

    public ElectricityBill(String consumerNo, String consumerName, int previousMonthReading, int currentMonthReading, String connectionType) {
        this.consumerNo = consumerNo;
        this.consumerName = consumerName;
        this.previousMonthReading = previousMonthReading;
        this.currentMonthReading = currentMonthReading;
        this.connectionType = connectionType;
    }

    public double calculateBill() {
        int unitsConsumed = currentMonthReading - previousMonthReading;
        double billAmount = 0;

        if (connectionType.equalsIgnoreCase("domestic")) {
            if (unitsConsumed <= 100) {
                billAmount = unitsConsumed * 1;
            } else if (unitsConsumed <= 200) {
                billAmount = 100 * 1 + (unitsConsumed - 100) * 2.5;
            } else if (unitsConsumed <= 500) {
                billAmount = 100 * 1 + 100 * 2.5 + (unitsConsumed - 200) * 4;
            } else {
                billAmount = 100 * 1 + 100 * 2.5 + 300 * 4 + (unitsConsumed - 500) * 6;
            }
        } else if (connectionType.equalsIgnoreCase("commercial")) {
            // Add commercial tariff logic here
        }

        return billAmount;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Enter consumer number:");
        String consumerNo = scanner.nextLine();

        System.out.println("Enter consumer name:");
        String consumerName = scanner.nextLine();

        System.out.println("Enter previous month reading:");
        int previousMonthReading = scanner.nextInt();

        System.out.println("Enter current month reading:");
        int currentMonthReading = scanner.nextInt();

        System.out.println("Enter connection type (domestic/commercial):");
        String connectionType = scanner.next();

        ElectricityBill bill = new ElectricityBill(consumerNo, consumerName, previousMonthReading, currentMonthReading, connectionType);

        double amount = bill.calculateBill();

        System.out.println("Consumer Number: " + consumerNo);
        System.out.println("Consumer Name: " + consumerName);
        System.out.println("Units Consumed: " + (currentMonthReading - previousMonthReading));
        System.out.println("Bill Amount: Ghc " + amount);
    }
}

