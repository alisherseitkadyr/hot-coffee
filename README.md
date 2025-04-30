# ☕ Hot Coffee - Coffee Shop Management System

A RESTful API backend for managing coffee shop operations, built with Go. Handles orders, menu items, inventory management, and sales reporting.

## Features

- **Layered Architecture**: Clean separation of concerns with handler-service-repository layers
- **JSON File Storage**: Persistent data storage in `data/` directory
- **Inventory Management**: Automatic stock deduction on order fulfillment
- **Automatic ID Generation**: Unique IDs for orders, menu items, and ingredients
- **RESTful API**: Standard HTTP methods and status codes
- **Logging**: Built-in logging with `log/slog`
- **Reporting**: Sales analytics and popular items tracking

## Getting Started

### Prerequisites
- Go 1.21+ 
- Make (optional)

### Installation
```bash
git clone https://github.com/alisherseitkadyr/hot-coffee.git
cd hot-coffee
go build -o hot-coffee .
Running
bash
./hot-coffee --port 8080 --dir data
API Documentation
Orders
Method	Path	Description
POST	/orders	Create new order
GET	/orders	List all orders
GET	/orders/{id}	Get specific order
PUT	/orders/{id}	Update order
DELETE	/orders/{id}	Delete order
POST	/orders/{id}/close	Close an order
Menu Items
Method	Path	Description
POST	/menu	Add new menu item
GET	/menu	List all menu items
GET	/menu/{id}	Get specific menu item
PUT	/menu/{id}	Update menu item
DELETE	/menu/{id}	Delete menu item
Inventory
Method	Path	Description
POST	/inventory	Add new inventory item
GET	/inventory	List all inventory items
GET	/inventory/{id}	Get specific inventory item
PUT	/inventory/{id}	Update inventory item
DELETE	/inventory/{id}	Delete inventory item
Reports
Method	Path	Description
GET	/reports/total-sales	Get total sales amount
GET	/reports/popular-items	List top 3 popular menu items
Example Usage
Create Order
bash
curl -X POST http://localhost:8080/orders \
  -H "Content-Type: application/json" \
  -d '{
    "customer_name": "John Doe",
    "items": [
      {
        "product_id": "latte",
        "quantity": 2
      }
    ]
  }'
Get Menu Items
bash
curl http://localhost:8080/menu
Add New Menu Item
bash
curl -X POST http://localhost:8080/menu \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Iced Coffee",
    "description": "Chilled coffee with milk",
    "price": 3.25,
    "ingredients": [
      {"ingredient_id": "coffee_beans", "quantity": 15},
      {"ingredient_id": "milk", "quantity": 100}
    ]
  }'
Check Inventory
bash
curl http://localhost:8080/inventory
Project Structure
hot-coffee/
├── cmd/
│   └── main.go            
├── internal/
│   ├── api/               
│   ├── service/         
│   └── repository/        
├── models/              
├── data/                 
│   ├── orders.json
│   ├── menu_items.json
│   └── inventory.json
├── go.mod
└── README.md
Data Storage
All data persisted in JSON files in data/ directory

Sample initial data created on first run:

menu_items.json: Contains espresso and latte

inventory.json: Contains coffee beans, water, and milk

orders.json: Empty array

Logging
Uses Go's log/slog package

Logs all operations with timestamps

Error details logged with context

Error Handling
Returns appropriate HTTP status codes:

400 Bad Request: Invalid input

404 Not Found: Resource not found

409 Conflict: Duplicate ID

500 Internal Server Error: Unexpected errors