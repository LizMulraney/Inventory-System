# ============= Capstone IV - Inventory ====================
from tabulate import tabulate


# define a class called shoes
class Shoes:

    def __init__(self, country, code, product, cost, quantity):
        self.country = country
        self.code = code
        self.product = product
        self.cost = int(cost)
        self.quantity = int(quantity)

    # return the cost of shoes
    def get_cost(self):
        return self.cost

    # return the quantity of shoes
    def get_quantity(self):
        return self.quantity

    # return a string representation of a class
    def __str__(self):
        return f"{self.country}, {self.code}, {self.product}, {str(self.cost)}, {str(self.quantity)}"


# =============Shoe list===========
shoe_list = []


# ==========Functions outside the class==============
def read_shoes_data():
    filename = None
    file_reads = True

    while filename is None:

        try:
            filename = open('inventory.txt', 'r')
            next(filename)

            for line in filename:
                if line.strip():
                    line = line.replace("\n", "")
                    new_shoes_list = line.split(",")
                    shoes_cls = Shoes(new_shoes_list[0], new_shoes_list[1], new_shoes_list[2],
                                      new_shoes_list[3], new_shoes_list[4])
                    shoe_list.append(shoes_cls)
        except FileNotFoundError:
            print("The inventory file cannot be found")

        except StopIteration:
            file_reads = False
            print("The inventory file is empty")

        finally:
            if filename is not None:
                filename.close()

            if file_reads is True and len(shoe_list) > 0:
                print("Shoes inventory loaded\n")
            else:
                print("Inventory load error")


def capture_shoes():
    if len(shoe_list) == 0:
        read_shoes_data()

    country_capture = input("Enter country: ")

    while True:
        code_capture = input("Enter code: ").upper()
        code_dupe = False

        for i in range(len(shoe_list)):
            if shoe_list[i].code == code_capture:
                code_dupe = True
                print("Code is already present, try a different code.")
                break
        if not code_dupe:
            break

    product_capture = input("Enter product name: ")

    while True:
        try:
            cost_capture = int(input("Enter cost: "))
            if cost_capture > 0:
                break
            else:
                print("Invalid input. Try again")

        except ValueError:
            print("Invalid input. Try again")

    while True:
        try:
            qty_capture = int(input("Enter stock quantity: "))
            if cost_capture > 0:
                break
            else:
                print("Invalid input. Try again")

        except ValueError:
            print("Invalid input. Try again")

    shoes_capture = Shoes(country_capture, code_capture, product_capture, cost_capture, qty_capture)
    shoe_list.append(shoes_capture)

    filename = open('inventory.txt', 'w')

    filename.write("Country,Code,Product,Cost,Quantity\n")

    for i in range(len(shoe_list)):
        line = shoe_list[i].__str__()
        line = line.replace(", ", ",") + "\n"
        filename.write(line)

    filename.close()

    print("\nShoe inventory item has been added")


def view_all():
    if len(shoe_list) == 0:
        read_shoes_data()

    if len(shoe_list) > 0:
        data = []
        with open('inventory.txt') as f:

            for line in f:
                data.append(list(map(str.strip, line.split(','))))

        print(tabulate(data, tablefmt='fancy_outline', headers='firstrow'))


# find shoe object with the lowest quantity
def re_stock():
    lowest_qty = None
    lowest_qty_index = None
    if len(shoe_list) == 0:
        read_shoes_data()

    if len(shoe_list) > 0:

        for i in range(len(shoe_list)):
            if i == 0 or shoe_list[i].quantity < lowest_qty.quantity:
                lowest_qty = shoe_list[i]
                lowest_qty_index = i

        table_list = [lowest_qty.__str__().split(", ")]

        print("Lowest quantity shoe inventory")
        print(tabulate(table_list, tablefmt='fancy_outline',
                       headers=["Country", "Code", "Product", "Cost", "Quantity"]))

        shoe_stock = input("Would you like to add stock to inventory? Y/N: ").lower()
        if shoe_stock == "":
            shoe_stock = " "

        if shoe_stock[0] == "y":
            while True:
                try:
                    shoe_stock_add = int(input("Enter number of shoes to add to stock: "))
                    shoe_list[lowest_qty_index].quantity = shoe_list[lowest_qty_index].quantity + shoe_stock_add

                    filename = open('inventory.txt', 'w')

                    filename.write("Country,Code,Product,Cost,Quantity\n")

                    for i in range(len(shoe_list)):
                        line = shoe_list[i].__str__()
                        line = line.replace(", ", ",") + "\n"
                        filename.write(line)

                    filename.close()

                    print("Shoe inventory updated")
                    break
                except ValueError:
                    print("Invalid input. Try again")

        elif shoe_stock[0] == "n":
            print("No stock to add. Main menu:\n")
        else:
            print("Invalid input. Main menu:\n")


# search for a shoe from the list using the search code
def search_shoe():
    if len(shoe_list) == 0:
        read_shoes_data()

    if len(shoe_list) > 0:
        search = input("Enter the shoe code to search: ").upper()

        find_code = False
        search_table = None

        for i in range(len(shoe_list)):
            if shoe_list[i].code == search:
                search_table = [shoe_list[i].__str__().split(", ")]
                find_code = True
                break

        if find_code:
            print("\nShoe inventory search results")
            print(tabulate(search_table, tablefmt='fancy_outline',
                           headers=["Country", "Code", "Product", "Cost", "Quantity"]))

        else:
            print("Code not found")


# calculate the total value for each item
def value_per_item():
    if len(shoe_list) == 0:
        read_shoes_data()

    if len(shoe_list) > 0:
        value_table = []
        print("\nShoe Inventory - Total Value\n")

        for i in range(len(shoe_list)):
            total_value = shoe_list[i].get_cost() * shoe_list[i].get_quantity()
            table_row = (shoe_list[i].__str__() + ", " + str(total_value)).split(", ")
            value_table.append(table_row)

        print(tabulate(value_table, tablefmt='fancy_outline',
                       headers=["Country", "Code", "Product", "Cost", "Quantity", "Total Value"]))


def highest_qty():
    highest_qty_cls = None
    if len(shoe_list) == 0:
        read_shoes_data()

    if len(shoe_list) > 0:
        for i in range(len(shoe_list)):
            if i == 0 or shoe_list[i].quantity > highest_qty_cls.quantity:
                highest_qty_cls = shoe_list[i]

        table_list = [highest_qty_cls.__str__().split(", ")]

        print("\nShoe Inventory - Highest Quantity")
        # print("Country      Code        Product     Cost        Quantity")
        print(tabulate(table_list, tablefmt='fancy_outline',
                       headers=["Country", "Code", "Product", "Cost", "Quantity", "Total Value"]))
        print(f"***** {highest_qty_cls.product} is on sale! *****\n")


# ==========Main Menu=============
if __name__ == '__main__':
    choice = 0
    while True:
        print("1. Read shoes data")
        print("2. Capture shoes")
        print("3. View all Shoes")
        print("4. Restock Shoes")
        print("5. Search Shoe")
        print("6. Get Total value of Stock")
        print("7. Highest Quantity")
        print("8. Quit")

        # get choice from user
        choice = int(input("Enter choice: "))

        # based on user choice call appropriate functions
        if choice == 1:
            read_shoes_data()
        elif choice == 2:
            capture_shoes()
        elif choice == 3:
            view_all()
        elif choice == 4:
            re_stock()
        elif choice == 5:
            search_shoe()
        elif choice == 6:
            value_per_item()
        elif choice == 7:
            highest_qty()
        elif choice == 8:
            print("Thank you.")
            break
        else:
            print("Invalid choice")
