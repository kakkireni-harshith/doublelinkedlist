# doublelinkedlist
class Node:
    def __init__(self, data):
        self.data = data
        self.prev = None
        self.next = None

class DoublyLinkedList:
    def __init__(self):
        self.head = None

    def insert_begin(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
        else:
            new_node.next = self.head
            self.head.prev = new_node
            self.head = new_node
        print(f"Inserted {value} at the beginning.")

    def insert_end(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
        else:
            temp = self.head
            while temp.next is not None:
                temp = temp.next
            temp.next = new_node
            new_node.prev = temp
        print(f"Inserted {value} at the end.")

    def insert_at_position(self, position, value):
        if position < 0:
            print("Invalid position.")
            return
        new_node = Node(value)
        if position == 0:
            new_node.next = self.head
            if self.head is not None:
                self.head.prev = new_node
            self.head = new_node
        else:
            temp = self.head
            for _ in range(position - 1):
                if temp is None:
                    print("Invalid position.")
                    return
                temp = temp.next
            if temp is None:
                print("Invalid position.")
                return
            new_node.next = temp.next
            new_node.prev = temp
            if temp.next is not None:
                temp.next.prev = new_node
            temp.next = new_node
        print(f"Inserted {value} at position {position}.")

    def delete_begin(self):
        if self.head is None:
            print("List is empty.")
            return
        if self.head.next is not None:
            self.head.next.prev = None
        self.head = self.head.next
        print("Deleted the first node.")

    def delete_end(self):
        if self.head is None:
            print("List is empty.")
            return
        temp = self.head
        while temp.next is not None:
            temp = temp.next
        if temp.prev is not None:
            temp.prev.next = None
        else:
            self.head = None
        print("Deleted the last node.")

    def delete_at_position(self, position):
        if self.head is None or position < 0:
            print("Invalid position.")
            return
        if position == 0:
            if self.head.next is not None:
                self.head.next.prev = None
            self.head = self.head.next
        else:
            temp = self.head
            for _ in range(position):
                if temp is None:
                    print("Invalid position.")
                    return
                temp = temp.next
            if temp is None:
                print("Invalid position.")
                return
            if temp.prev is not None:
                temp.prev.next = temp.next
            if temp.next is not None:
                temp.next.prev = temp.prev
        print(f"Deleted node at position {position}.")

    def search_node(self, value):
        temp = self.head
        pos = 0
        while temp is not None:
            if temp.data == value:
                print(f"Element {value} found at position {pos}.")
                return
            temp = temp.next
            pos += 1
        print(f"Element {value} not found in the list.")

    def count_nodes(self):
        temp = self.head
        count = 0
        while temp is not None:
            count += 1
            temp = temp.next
        print(f"Number of nodes: {count}")

    def display_list(self):
        temp = self.head
        print("List:", end=" ")
        while temp is not None:
            print(temp.data, end=" ")
            temp = temp.next
        print()

if __name__ == "__main__":
    linked_list = DoublyLinkedList()
    
    while True:
        print("\nDoubly Linked List Operations")
        print("1. Insert at beginning")
        print("2. Insert at end")
        print("3. Insert at a position")
        print("4. Delete from beginning")
        print("5. Delete from end")
        print("6. Delete from a position")
        print("7. Search for an element")
        print("8. Count the number of nodes")
        print("9. Display list")
        print("10. Exit")
        
        choice = int(input("Enter your choice: "))
        
        if choice == 1:
            value = int(input("Enter value to insert: "))
            linked_list.insert_begin(value)
        elif choice == 2:
            value = int(input("Enter value to insert: "))
            linked_list.insert_end(value)
        elif choice == 3:
            position = int(input("Enter position to insert: "))
            value = int(input("Enter value to insert: "))
            linked_list.insert_at_position(position, value)
        elif choice == 4:
            linked_list.delete_begin()
        elif choice == 5:
            linked_list.delete_end()
        elif choice == 6:
            position = int(input("Enter position to delete: "))
            linked_list.delete_at_position(position)
        elif choice == 7:
            value = int(input("Enter value to search: "))
            linked_list.search_node(value)
        elif choice == 8:
            linked_list.count_nodes()
        elif choice == 9:
            linked_list.display_list()
        elif choice == 10:
            break
        else:
            print("Invalid choice.")
