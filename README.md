# HOTEL-CARD-
HOTEL MENU CARD USING R SOFTWARE

# Define the hotel menu with food items and costs
menu <- data.frame(
  Item = c("Burger", "Pizza", "Pasta", "Salad", "Soda"),
  Cost = c(10.99, 12.99, 8.99, 5.99, 2.49)
)

# Function to display the hotel menu
display_menu <- function(menu) {
  cat("\n==== Hotel Menu ====\n")
  print(menu)
}

# Function to take user input for ordering
order_food <- function(menu) {
  selected_items <- c()
  
  while (TRUE) {
    display_menu(menu)
    cat("\nEnter the number of the item you want to order (or '0' to finish): ")
    
    # Read user input
    choice <- as.numeric(readline(prompt = ""))
    
    # Check if the input is a valid number
    if (is.na(choice)) {
      cat("Invalid input. Please enter a number.\n")
      next
    }
    
    # Check if the input is '0' to finish ordering
    if (choice == 0) {
      break
    } else if (choice >= 1 && choice <= nrow(menu)) {
      # Add the selected item to the list
      selected_items <- c(selected_items, choice)
      cat(paste("Added '", menu$Item[choice], "' to your order.\n", sep = ""))
    } else {
      cat("Invalid choice. Please enter a valid item number.\n")
    }
  }
  
  return(selected_items)
}

# Function to calculate the total cost of the selected items
calculate_total_cost <- function(selected_items, menu) {
  total_cost <- sum(menu$Cost[selected_items])
  return(total_cost)
}

# Order food
selected_items <- order_food(menu)

# Calculate and display the total cost
if (length(selected_items) > 0) {
  total_cost <- calculate_total_cost(selected_items, menu)
  cat("\nYour order total is: $", round(total_cost, 2), "\n")
} else {
  cat("\nNo items were selected. Thank you!\n")
}
