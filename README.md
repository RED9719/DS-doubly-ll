# DS-doubly-ll
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None

class DoublyLinkedList:
    def __init__(self):
        self.head = None

    def traverse(self):
        current = self.head
        while current:
            print(current.data, end=" <-> ")
            current = current.next
        print("None")

    def insert_at_beginning(self, data):
        new_node = Node(data)
        if self.head is not None:
            self.head.prev = new_node
        new_node.next = self.head
        self.head = new_node

    def insert_at_end(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
            return
        last_node = self.head
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        new_node.prev = last_node

    def insert_at_position(self, position, data):
        if position < 0:
            print("Invalid position!")
            return
        new_node = Node(data)
        if position == 0:
            self.insert_at_beginning(data)
            return
        current = self.head
        for _ in range(position - 1):
            if not current:
                print("Position out of bounds!")
                return
            current = current.next
        new_node.next = current.next
        if current.next:
            current.next.prev = new_node
        current.next = new_node
        new_node.prev = current

    def delete_from_beginning(self):
        if self.head is None:
            print("List is empty!")
            return
        self.head = self.head.next
        if self.head:
            self.head.prev = None

    def delete_from_end(self):
        if self.head is None:
            print("List is empty!")
            return
        if self.head.next is None:
            self.head = None
            return
        last_node = self.head
        while last_node.next:
            last_node = last_node.next
        last_node.prev.next = None

    def delete_from_position(self, position):
        if position < 0 or self.head is None:
            print("Invalid position or list is empty!")
            return
        if position == 0:
            self.delete_from_beginning()
            return
        current = self.head
        for _ in range(position):
            if not current.next:
                print("Position out of bounds!")
                return
            current = current.next
        if current.next:
            current.next.prev = current.prev
        if current.prev:
            current.prev.next = current.next
if __name__ == "__main__":
    dll = DoublyLinkedList()
    dll.insert_at_beginning(10)
    dll.insert_at_end(20)
    dll.insert_at_end(30)
    dll.insert_at_position(1, 15)
    print("Linked List after insertion:")
    dll.traverse()

    dll.delete_from_beginning()
    print("\nLinked List after deletion from beginning:")
    dll.traverse()

    dll.delete_from_end()
    print("\nLinked List after deletion from end:")
    dll.traverse()

    dll.delete_from_position(1)
    print("\nLinked List after deletion from position 1:")
    dll.traverse()
