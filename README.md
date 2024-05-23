

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.util.HashMap;
import java.util.Map;

public class Bistro implements FoodMenu {
    private JFrame frame;
    private JTextArea textArea;
    private JButton orderButton;
    private Map<String, FoodItem> menuItems;

    public Bistro() {
        frame = new JFrame("Bistro");
        frame.setSize(500, 400);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new BorderLayout());

        textArea = new JTextArea();
        textArea.setEditable(false);
        frame.add(textArea, BorderLayout.CENTER);

        orderButton = new JButton("Place Order");
        orderButton.addActionListener((ActionEvent e) -> {
            String inputPassword = JOptionPane.showInputDialog(frame, "Enter password:");
            if (inputPassword != null && inputPassword.equals("malik111")) {
                placeOrder();
            } else {
                JOptionPane.showMessageDialog(frame, "Incorrect password!", "Error", JOptionPane.ERROR_MESSAGE);
            }
        });

        frame.add(orderButton, BorderLayout.SOUTH);

        menuItems = new HashMap<>();
        menuItems.put("1", new Pizza("Chicken Fazita", 700));
        menuItems.put("2", new Burger("Zinger Burger", 250));
        menuItems.put("3", new Sandwich("Club Sandwich", 220));
        menuItems.put("4", new Roll("Chicken Roll", 50));
        menuItems.put("5", new Biryani("Chicken Biryani", 300));
    }

    @Override
    public void displayMenu() {
        textArea.setText("Welcome to Bistro!\n");
        for (Map.Entry<String, FoodItem> entry : menuItems.entrySet()) {
            textArea.append(entry.getKey() + ") " + entry.getValue().getDescription() + " - " + entry.getValue().getPrice() + "\n");
        }
    }

    private void placeOrder() {
        String choice = JOptionPane.showInputDialog(frame, "Enter your choice:");
        if (choice == null) {
            return;
        }

        FoodItem selectedItem = menuItems.get(choice);
        if (selectedItem == null) {
            JOptionPane.showMessageDialog(frame, "Invalid choice!", "Error", JOptionPane.ERROR_MESSAGE);
            return;
        }

        String quantity = JOptionPane.showInputDialog(frame, "Enter quantity:");
        if (quantity == null || quantity.isEmpty()) {
            return;
        }

        int quantityValue = Integer
