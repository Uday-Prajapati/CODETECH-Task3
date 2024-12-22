/* TASK THREE:INVENTORY MANAGEMENT SYSTEM
 Build a Java program to manage inventory for a store or warehouse. The system should
 allow users to add, edit, and delete products, track inventory levels, and generate reports
 such as low- stock alerts or sales summaries. Implement features like user authentication,
 data validation, and graphical user interface (GUI) for better usability. */

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.*;
// Product class to manage individual products
class Product {
    private String id;
    private String name;
    private int quantity;
    private double price;

    public Product(String id, String name, int quantity, double price) {
        this.id = id;
        this.name = name;
        this.quantity = quantity;
        this.price = price;
    }

    public String getId() { return id; }
    public String getName() { return name; }
    public int getQuantity() { return quantity; }
    public double getPrice() { return price; }

    public void setName(String name) { this.name = name; }
    public void setQuantity(int quantity) { this.quantity = quantity; }
    public void setPrice(double price) { this.price = price; }

    @Override
    public String toString() {
        return String.format("ID: %s, Name: %s, Quantity: %d, Price: %.2f", id, name, quantity, price);
    }
}

// Inventory Management System with Authentication
public class InventoryManagementSystem {
    private Map<String, Product> inventory;
    private Map<String, String> users;

    public InventoryManagementSystem() {
        inventory = new HashMap<>();
        users = new HashMap<>();
        // Predefined users (username:password)
        users.put("admin", "password123");
        users.put("user", "12345");

        initLoginGUI();
    }

    // Initialize Login GUI
    private void initLoginGUI() {
        JFrame loginFrame = new JFrame("Login");
        loginFrame.setSize(300, 150);
        loginFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(3, 2));

        JLabel usernameLabel = new JLabel("Username:");
        JTextField usernameField = new JTextField();
        JLabel passwordLabel = new JLabel("Password:");
        JPasswordField passwordField = new JPasswordField();
        JButton loginButton = new JButton("Login");

        panel.add(usernameLabel);
        panel.add(usernameField);
        panel.add(passwordLabel);
        panel.add(passwordField);
        panel.add(new JLabel());
        panel.add(loginButton);

        loginFrame.add(panel);
        loginFrame.setVisible(true);

        loginButton.addActionListener(e -> {
            String username = usernameField.getText();
            String password = new String(passwordField.getPassword());
            if (authenticate(username, password)) {
                loginFrame.dispose();
                initInventoryGUI();
            } else {
                JOptionPane.showMessageDialog(loginFrame, "Invalid credentials", "Error", JOptionPane.ERROR_MESSAGE);
            }
        });
    }

    // Authenticate User
    private boolean authenticate(String username, String password) {
        return users.containsKey(username) && users.get(username).equals(password);
    }

    // Initialize Inventory GUI
    private void initInventoryGUI() {
        JFrame frame = new JFrame("Inventory Management System");
        frame.setSize(600, 400);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(0, 2));

        JLabel idLabel = new JLabel("Product ID:");
        JTextField idField = new JTextField();
        JLabel nameLabel = new JLabel("Product Name:");
        JTextField nameField = new JTextField();
        JLabel quantityLabel = new JLabel("Quantity:");
        JTextField quantityField = new JTextField();
        JLabel priceLabel = new JLabel("Price:");
        JTextField priceField = new JTextField();

        JButton addButton = new JButton("Add Product");
        JButton editButton = new JButton("Edit Product");
        JButton deleteButton = new JButton("Delete Product");
        JButton reportButton = new JButton("Generate Report");

        JTextArea outputArea = new JTextArea();
        outputArea.setEditable(false);

        panel.add(idLabel);
        panel.add(idField);
        panel.add(nameLabel);
        panel.add(nameField);
        panel.add(quantityLabel);
        panel.add(quantityField);
        panel.add(priceLabel);
        panel.add(priceField);
        panel.add(addButton);
        panel.add(editButton);
        panel.add(deleteButton);
        panel.add(reportButton);

        frame.add(panel, BorderLayout.NORTH);
        frame.add(new JScrollPane(outputArea), BorderLayout.CENTER);

        // Add Product Button Action
        addButton.addActionListener(e -> {
            String id = idField.getText();
            String name = nameField.getText();
            int quantity;
            double price;
            try {
                quantity = Integer.parseInt(quantityField.getText());
                price = Double.parseDouble(priceField.getText());
            } catch (NumberFormatException ex) {
                JOptionPane.showMessageDialog(frame, "Invalid quantity or price", "Error", JOptionPane.ERROR_MESSAGE);
                return;
            }

            if (inventory.containsKey(id)) {
                JOptionPane.showMessageDialog(frame, "Product ID already exists", "Error", JOptionPane.ERROR_MESSAGE);
                return;
            }

            inventory.put(id, new Product(id, name, quantity, price));
            outputArea.append("Product added: " + name + "\n");
        });

        // Edit Product Button Action
        editButton.addActionListener(e -> {
            String id = idField.getText();
            if (!inventory.containsKey(id)) {
                JOptionPane.showMessageDialog(frame, "Product ID not found", "Error", JOptionPane.ERROR_MESSAGE);
                return;
            }

            Product product = inventory.get(id);
            product.setName(nameField.getText());
            try {
                product.setQuantity(Integer.parseInt(quantityField.getText()));
                product.setPrice(Double.parseDouble(priceField.getText()));
            } catch (NumberFormatException ex) {
                JOptionPane.showMessageDialog(frame, "Invalid quantity or price", "Error", JOptionPane.ERROR_MESSAGE);
                return;
            }
            outputArea.append("Product updated: " + id + "\n");
        });

        // Delete Product Button Action
        deleteButton.addActionListener(e -> {
            String id = idField.getText();
            if (inventory.remove(id) != null) {
                outputArea.append("Product removed: " + id + "\n");
            } else {
                JOptionPane.showMessageDialog(frame, "Product ID not found", "Error", JOptionPane.ERROR_MESSAGE);
            }
        });

        // Generate Report Button Action
        reportButton.addActionListener(e -> {
            outputArea.append("\nInventory Report:\n");
            for (Product product : inventory.values()) {
                outputArea.append(product.toString() + "\n");
                if (product.getQuantity() < 5) {
                    outputArea.append("Low stock alert for " + product.getName() + "\n");
                }
            }
        });

        frame.setVisible(true);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(InventoryManagementSystem::new);
    }
}
