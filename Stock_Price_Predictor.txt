import java.util.ArrayList;
import java.util.Scanner;

class StockData {
    String name;
    ArrayList<Double> history;

    StockData(String name) {
        this.name = name;
        this.history = new ArrayList<>();
    }
}

public class stockpricepredictor {

    static Scanner sc = new Scanner(System.in);
    static ArrayList<StockData> stocks = new ArrayList<>();


    static int findStock(String name) {
        for (int i = 0; i < stocks.size(); i++) {
            if (stocks.get(i).name.equals(name))
                return i;
        }
        return -1;
    }


    static double calculateSMA(ArrayList<Double> d, int p) {
        if (p <= 0 || d.size() < p)
            return 0;

        double sum = 0;

        for (int i = d.size() - p; i < d.size(); i++) {
            sum += d.get(i);
        }

        return sum / p;
    }


    static double calculateEMA(ArrayList<Double> d, int p) {
        if (p <= 0 || d.size() < p)
            return 0;

        double k = 2.0 / (p + 1);

        ArrayList<Double> first = new ArrayList<>(
            d.subList(0, p)
        );

        double ema = calculateSMA(first, p);

        for (int i = p; i < d.size(); i++) {
            ema = (d.get(i) - ema) * k + ema;
        }

        return ema;
    }


    static double calculateMomentum(ArrayList<Double> d, int p) {
        if (p <= 0 || d.size() <= p)
            return 0;

        return d.get(d.size() - 1)
             - d.get(d.size() - 1 - p);
    }


    static double calculateSlope(ArrayList<Double> d) {
        int n = d.size();

        if (n < 2)
            return 0;

        double sx = 0, sy = 0;
        double sxy = 0, sx2 = 0;

        for (int i = 0; i < n; i++) {
            sx += i;
            sy += d.get(i);
            sxy += i * d.get(i);
            sx2 += i * i;
        }

        double den = n * sx2 - sx * sx;

        if (Math.abs(den) < 1e-9)
            return 0;

        return (n * sxy - sx * sy) / den;
    }


    static double predictNextPrice(ArrayList<Double> d) {
        if (d.size() < 2) {
            return d.isEmpty() ? 0 : d.get(d.size() - 1);
        }

        return d.get(d.size() - 1) + calculateSlope(d);
    }


    static void addStock() {
        System.out.print("Enter stock name: ");
        String name = sc.next();

        if (findStock(name) != -1) {
            System.out.println("Stock already exists!");
            return;
        }

        System.out.print("Number of historical prices: ");

        int n;

        if (!sc.hasNextInt()) {
            System.out.println("Invalid entries!");
            sc.next();
            return;
        }

        n = sc.nextInt();

        if (n <= 0) {
            System.out.println("Invalid entries!");
            return;
        }

        StockData s = new StockData(name);

        for (int i = 0; i < n; i++) {
            System.out.print("Price " + (i + 1) + ": ");

            if (!sc.hasNextDouble()) {
                System.out.println("Invalid price; data not saved.");
                sc.next();
                return;
            }

            double price = sc.nextDouble();

            if (!Double.isFinite(price) || price <= 0) {
                System.out.println("Invalid price; data not saved.");
                return;
            }

            s.history.add(price);
        }

        stocks.add(s);

        System.out.println("Stock data loaded successfully!");
    }


    static int requestStock() {
        System.out.print("Enter stock name: ");
        String name = sc.next();

        int i = findStock(name);

        if (i == -1)
            System.out.println("Stock not found!");

        return i;
    }


    static void showIndicators() {
        int i = requestStock();

        if (i == -1)
            return;

        ArrayList<Double> d = stocks.get(i).history;

        System.out.printf(
            "Latest: Rs.%.2f%n", d.get(d.size() - 1)
        );

        System.out.printf("SMA(5): %.2f%n", calculateSMA(d, 5));
        System.out.printf("EMA(5): %.2f%n", calculateEMA(d, 5));
        System.out.printf("Momentum(3): %.2f%n", calculateMomentum(d, 3));
        System.out.printf("Trend slope: %.2f%n", calculateSlope(d));
    }


    static void predictPrice() {
        int i = requestStock();

        if (i == -1)
            return;

        ArrayList<Double> d = stocks.get(i).history;

        double current = d.get(d.size() - 1);
        double forecast = predictNextPrice(d);

        System.out.printf("Current: Rs.%.2f%n", current);
        System.out.printf("Predicted: Rs.%.2f%n", forecast);

        if (forecast > current)
            System.out.println("Upward trend");
        else if (forecast < current)
            System.out.println("Downward trend");
        else
            System.out.println("Flat trend");
    }


    static void showHistory() {
        int i = requestStock();

        if (i == -1)
            return;

        System.out.print("History: ");

        for (double p : stocks.get(i).history) {
            System.out.print(p + " ");
        }

        System.out.println();
    }


    static void accuracyReport() {
        int i = requestStock();

        if (i == -1)
            return;

        ArrayList<Double> d = stocks.get(i).history;

        if (d.size() < 3) {
            System.out.println("Insufficient data.");
            return;
        }

        ArrayList<Double> train = new ArrayList<>(
            d.subList(0, d.size() - 1)
        );

        double actual = d.get(d.size() - 1);
        double pred = predictNextPrice(train);

        double score = 100 - Math.abs(actual - pred) / actual * 100;

        System.out.printf("Approximate score: %.2f%%%n", score);
    }


    static void report() {
        if (stocks.isEmpty()) {
            System.out.println("No stock data available.");
            return;
        }

        for (StockData s : stocks) {
            ArrayList<Double> d = s.history;

            System.out.println("\nStock: " + s.name);

            System.out.printf("Latest: Rs.%.2f%n",
                d.get(d.size() - 1));

            System.out.printf("SMA: %.2f%n", calculateSMA(d, 5));
            System.out.printf("EMA: %.2f%n", calculateEMA(d, 5));
            System.out.printf("Momentum: %.2f%n", calculateMomentum(d, 3));

            System.out.printf("Forecast: Rs.%.2f%n",
                predictNextPrice(d));
        }
    }


    static void displayAllStocks() {
        if (stocks.isEmpty()) {
            System.out.println("No stocks loaded.");
            return;
        }

        for (StockData s : stocks) {
            System.out.printf(
                "%s | Latest: Rs.%.2f | Entries: %d%n",
                s.name,
                s.history.get(s.history.size() - 1),
                s.history.size()
            );
        }
    }


    static void showPriceChange() {
        int i = requestStock();

        if (i == -1)
            return;

        ArrayList<Double> d = stocks.get(i).history;

        double change = d.get(d.size() - 1) - d.get(0);
        double pct = change / d.get(0) * 100;

        System.out.printf("Absolute change: Rs.%.2f%n", change);
        System.out.printf("Percentage change: %.2f%%%n", pct);
    }


    static void compareStocks() {
        System.out.print("First stock: ");
        String a = sc.next();

        int i = findStock(a);

        System.out.print("Second stock: ");
        String b = sc.next();

        int j = findStock(b);

        if (i == -1 || j == -1 || i == j) {
            System.out.println("Invalid stock selection.");
            return;
        }

        int[] indexes = {i, j};

        for (int k : indexes) {
            StockData s = stocks.get(k);

            System.out.printf(
                "%s | Latest: Rs.%.2f | Slope: %.2f%n",
                s.name,
                s.history.get(s.history.size() - 1),
                calculateSlope(s.history)
            );
        }
    }


    static void deleteStock() {
        int i = requestStock();

        if (i == -1)
            return;

        System.out.print("Confirm deletion (y/n): ");
        char c = sc.next().charAt(0);

        if (c == 'y' || c == 'Y') {
            stocks.remove(i);
            System.out.println("Stock deleted.");
        } else {
            System.out.println("Deletion cancelled.");
        }
    }


    public static void main(String[] args) {

        int choice=-1;

        do {
            System.out.println("\n=== STOCK PRICE PREDICTOR ===");
            System.out.println("1. Load Stock Data");
            System.out.println("2. Technical Indicators");
            System.out.println("3. Predict Next Price");
            System.out.println("4. Show Price History");
            System.out.println("5. Prediction Score");
            System.out.println("6. Forecast Report");
            System.out.println("7. Display All Stocks");
            System.out.println("8. Calculate Price Change");
            System.out.println("9. Compare Two Stocks");
            System.out.println("10. Delete Stock Data");
            System.out.println("0. Exit");
            System.out.print("Choice: ");

            if (!sc.hasNextInt()) {
                System.out.println("Invalid input!");
                sc.next();
                continue;
            }

            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    addStock();
                    break;

                case 2:
                    showIndicators();
                    break;

                case 3:
                    predictPrice();
                    break;

                case 4:
                    showHistory();
                    break;

                case 5:
                    accuracyReport();
                    break;

                case 6:
                    report();
                    break;

                case 7:
                    displayAllStocks();
                    break;

                case 8:
                    showPriceChange();
                    break;

                case 9:
                    compareStocks();
                    break;

                case 10:
                    deleteStock();
                    break;

                case 0:
                    System.out.println("Thank you!");
                    break;

                default:
                    System.out.println("Invalid choice!");
            }

        } while (choice != 0);

        sc.close();
    }
}