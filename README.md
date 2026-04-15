# cafeflow-order-system

        ArrayList<String> coffees = new ArrayList<>(Arrays.asList(
                "Nescafe", "Kopiko Blanka", "Creamy White", "Coffee Mate"
        ));
        ArrayList<Integer> prices = new ArrayList<>(Arrays.asList(
                30, 45, 25, 35
        ));

        Set<String> occupiedTables = new HashSet<>();

        System.out.println("=== WELCOME TO OUR CAFE ===");

        while (true) {
            System.out.print("\nLog in as (admin/customer/exit): ");
            String role = sc.nextLine().trim().toLowerCase();

            if (role.equals("exit")) {
                System.out.println("System closed.");
                break;
            }

            if (!role.equals("admin") && !role.equals("customer")) {
                System.out.println("Invalid role!");
                continue;
            }

            if (role.equals("admin")) {
                System.out.print("Enter admin password: ");
                String pass = sc.nextLine().trim();
                if (!pass.equals("1234")) {
                    System.out.println("Access Denied!");
                    continue;
                }

                while (true) {
                    System.out.println("\n--- ADMIN MENU ---");
                    System.out.println("1. Add Coffee");
                    System.out.println("2. Change Price");
                    System.out.println("3. Back");

                    int choice;
                    try {
                        System.out.print("Choose option: ");
                        choice = Integer.parseInt(sc.nextLine());
                    } catch (Exception e) {
                        System.out.println("Invalid input!");
                        continue;
                    }

                    if (choice == 1) {
                        String newCoffee = "";
                        while (true) {
                            System.out.print("Enter new coffee name: ");
                            newCoffee = sc.nextLine().trim();
                            if (!newCoffee.isEmpty()) break;
                            System.out.println("Coffee name cannot be empty!");
                        }

                        int newPrice = 0;
                        while (true) {
                            System.out.print("Enter price: ");
                            try {
                                newPrice = Integer.parseInt(sc.nextLine());
                                if (newPrice > 0) break;
                            } catch (Exception e) {}
                            System.out.println("Invalid price!");
                        }

                        coffees.add(newCoffee);
                        prices.add(newPrice);
                        System.out.println("Coffee Added Successfully!");

                    } else if (choice == 2) {
                        for (int i = 0; i < coffees.size(); i++) {
                            System.out.println((i + 1) + ". " + coffees.get(i) + " - PHP" + prices.get(i));
                        }

                        int index = -1;
                        while (true) {
                            System.out.print("Select coffee to change price: ");
                            try {
                                index = Integer.parseInt(sc.nextLine()) - 1;
                                if (index >= 0 && index < coffees.size()) break;
                            } catch (Exception e) {}
                            System.out.println("Invalid selection!");
                        }

                        int newPrice = 0;
                        while (true) {
                            System.out.print("Enter new price: ");
                            try {
                                newPrice = Integer.parseInt(sc.nextLine());
                                if (newPrice > 0) break;
                            } catch (Exception e) {}
                            System.out.println("Invalid price!");
                        }

                        prices.set(index, newPrice);
                        System.out.println("Price Updated!");

                    } else if (choice == 3) {
                        break; 
                    } else {
                        System.out.println("Invalid choice!");
                    }
                }

                continue; 

            }

            System.out.print("Enter Your Name: ");
            String name = "";
            while (true) {
                name = sc.nextLine().trim();
                if (!name.isEmpty()) break;
                System.out.print("Invalid! Enter your name again: ");
            }

            String table = "";
            while (true) {
                System.out.print("Enter Table Number (1-8): ");
                table = sc.nextLine().trim();

                if (!table.matches("[1-8]")) {
                    System.out.println("Invalid! Only 1-8 allowed.");
                    continue;
                }

                if (occupiedTables.contains(table)) {
                    System.out.println("Sorry! Table " + table + " is already occupied. Choose another table.");
                    continue;
                }

                occupiedTables.add(table); 
                break;
            }

            System.out.println("\nHello " + name + ", your table is #" + table);

            while (true) {
                System.out.print("\nDo you want to order? (yes/no): ");
                String answer = sc.nextLine().trim().toLowerCase();
                if (answer.equals("no")) break;
                if (!answer.equals("yes")) continue;

                System.out.println("\n=== MENU ===");
                for (int i = 0; i < coffees.size(); i++) {
                    System.out.println((i + 1) + ". " + coffees.get(i) + " - PHP" + prices.get(i));
                }

                int index = -1;
                while (true) {
                    System.out.print("Select coffee (number): ");
                    try {
                        index = Integer.parseInt(sc.nextLine()) - 1;
                        if (index >= 0 && index < coffees.size()) break;
                    } catch (Exception e) {}
                    System.out.println("Invalid selection!");
                }

                String selectedCoffee = coffees.get(index);
                int selectedPrice = prices.get(index);

                int qty = 0;
                while (true) {
                    System.out.print("Quantity: ");
                    try {
                        qty = Integer.parseInt(sc.nextLine());
                        if (qty > 0) break;
                    } catch (Exception e) {}
                    System.out.println("Invalid quantity!");
                }

                int total = qty * selectedPrice;

                System.out.println("\n--- RECEIPT ---");
                System.out.println("Name: " + name);
                System.out.println("Table: " + table);
                System.out.println("Order: " + selectedCoffee + " x" + qty);
                System.out.println("Total: PHP" + total);

                System.out.print("Order again? (yes/no): ");
            
                if (!sc.nextLine().trim().equalsIgnoreCase("yes"))
                System.out.println("\n=== THANK YOU FOR PURCHASING ===");
                break;
            }
        }
    }
}
