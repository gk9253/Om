#include <iostream>
#include <vector>
#include <iomanip>

using namespace std;

// Product structure
struct Product {
    string name;
    int quantity;
    double price;
};

// Global variables
vector<Product> inventory;
double totalSales = 0.0;

// Function to add a new product to the inventory
void addProduct() {
    Product product;
    cout << "\nEnter product name: ";
    cin >> product.name;
    cout << "Enter product quantity: ";
    cin >> product.quantity;
    cout << "Enter product price: ";
    cin >> product.price;
    inventory.push_back(product);
    cout << "Product added successfully!\n";
}

// Function to display the current inventory
void viewInventory() {
    cout << "\nCurrent Inventory:\n";
    cout << left << setw(15) << "Name" 
         << setw(10) << "Quantity" 
         << setw(10) << "Price" << endl;
    for (const auto& product : inventory) {
        cout << left << setw(15) << product.name 
             << setw(10) << product.quantity 
             << setw(10) << product.price << endl;
    }
}

// Function to sell a product
void sellProduct() {
    string productName;
    int sellQuantity;
    cout << "\nEnter product name to sell: ";
    cin >> productName;
    cout << "Enter quantity to sell: ";
    cin >> sellQuantity;

    for (auto& product : inventory) {
        if (product.name == productName) {
            if (product.quantity >= sellQuantity) {
                product.quantity -= sellQuantity;
                double saleAmount = sellQuantity * product.price;
                totalSales += saleAmount;
                cout << "Product sold successfully! Sales amount: " 
                     << saleAmount << endl;
            } else {
                cout << "Insufficient stock available!\n";
            }
            return;
        }
    }
    cout << "Product not found in inventory!\n";
}

// Function to view total sales
void viewSales() {
    cout << "\nTotal Sales: " << totalSales << endl;
}

// Main menu
void menu() {
    int choice;
    do {
        cout << "\n--- Small Business Inventory & Sales Tracker ---\n";
        cout << "1. Add Product\n";
        cout << "2. View Inventory\n";
        cout << "3. Sell Product\n";
        cout << "4. View Total Sales\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                addProduct();
                break;
            case 2:
                viewInventory();
                break;
            case 3:
                sellProduct();
                break;
            case 4:
                viewSales();
                break;
            case 5:
                cout << "Exiting program. Thank you!\n";
                break;
            default:
                cout << "Invalid choice! Please try again.\n";
        }
    } while (choice != 5);
}

int main() {
    menu();
    return 0;
}
