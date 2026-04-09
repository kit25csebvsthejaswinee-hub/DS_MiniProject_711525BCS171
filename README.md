import java.util.Scanner;

class Product {
    String name;
    int quantity;

    Product(String name, int quantity) {
        this.name = name;
        this.quantity = quantity;
    }
}

public class Miniproject {

    static void heapify(Product arr[], int n, int i) {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;

        if (left < n && arr[left].quantity > arr[largest].quantity)
            largest = left;

        if (right < n && arr[right].quantity > arr[largest].quantity)
            largest = right;

        if (largest != i) {
            Product temp = arr[i];
            arr[i] = arr[largest];
            arr[largest] = temp;

            heapify(arr, n, largest);
        }
    }

    static void heapSort(Product arr[], int n) {
        for (int i = n / 2 - 1; i >= 0; i--)
            heapify(arr, n, i);

        for (int i = n - 1; i > 0; i--) {
            Product temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            heapify(arr, i, 0);
        }
    }

    static void display(Product arr[], int n) {
        System.out.println("\nProducts sorted by quantity:");
        for (int i = 0; i < n; i++) {
            System.out.println(arr[i].name + " - " + arr[i].quantity);
        }
    }

    static void search(Product arr[], int n, String key) {
        boolean found = false;

        for (int i = 0; i < n; i++) {
            if (arr[i].name.equalsIgnoreCase(key)) {
                System.out.println("Product Found!");
                System.out.println("Quantity: " + arr[i].quantity);
                found = true;
                break;
            }
        }

        if (!found) {
            System.out.println("Product not found.");
        }
    }

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of products: ");
        int n = sc.nextInt();
        sc.nextLine();

        Product[] arr = new Product[n];

        for (int i = 0; i < n; i++) {
            System.out.print("Enter product name: ");
            String name = sc.nextLine();

            System.out.print("Enter quantity: ");
            int qty = sc.nextInt();
            sc.nextLine();

            arr[i] = new Product(name, qty);
        }

        heapSort(arr, n);
        display(arr, n);

        System.out.print("\nEnter product name to search: ");
        String key = sc.nextLine();

        search(arr, n, key);

        sc.close();
    }
}
