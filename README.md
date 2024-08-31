# book-and-ebook-classes-Python
n this task, we designed a class structure to handle both traditional printed books and digital ebooks, focusing on managing book attributes and calculating author royalties with different rules for physical and digital formats.
class Book:
    def __init__(self, title, author, publisher, price):
        self._title = title
        self._author = author
        self._publisher = publisher
        self._price = price
        self._copies_sold = 0  # Track number of copies sold

    # Getter and setter properties for title
    @property
    def title(self):
        return self._title

    @title.setter
    def title(self, value):
        self._title = value

    # Getter and setter properties for author
    @property
    def author(self):
        return self._author

    @author.setter
    def author(self, value):
        self._author = value

    # Getter and setter properties for publisher
    @property
    def publisher(self):
        return self._publisher

    @publisher.setter
    def publisher(self, value):
        self._publisher = value

    # Getter and setter properties for price
    @property
    def price(self):
        return self._price

    @price.setter
    def price(self, value):
        self._price = value

    # Getter and setter properties for copies_sold
    @property
    def copies_sold(self):
        return self._copies_sold

    @copies_sold.setter
    def copies_sold(self, value):
        self._copies_sold = value

    # Method to calculate royalty
    def royalty(self):
        royalty_amount = 0
        if self._copies_sold <= 500:
            royalty_amount = 0.10 * self._price * self._copies_sold
        elif self._copies_sold <= 1500:
            royalty_amount = (0.10 * self._price * 500) + (0.125 * self._price * (self._copies_sold - 500))
        else:
            royalty_amount = (0.10 * self._price * 500) + (0.125 * self._price * 1000) + \
                             (0.15 * self._price * (self._copies_sold - 1500))
        return royalty_amount

# Subclass 'Ebook' inherited from 'Book'
class Ebook(Book):
    def __init__(self, title, author, publisher, price, format):
        super().__init__(title, author, publisher, price)
        self._format = format

    # Getter and setter properties for format
    @property
    def format(self):
        return self._format

    @format.setter
    def format(self, value):
        self._format = value

    # Overriding royalty() method for Ebook
    def royalty(self):
        royalty_amount = super().royalty()  # Calculate royalty using parent class method
        gst_deduction = 0.12 * royalty_amount  # GST deduction on ebook
        return royalty_amount - gst_deduction

# Example Usage:
book = Book("Python 101", "John Doe", "TechPress", 1000)
book.copies_sold = 2000
print(f"Royalty for book: {book.royalty()}")

ebook = Ebook("Python 101 - Ebook", "John Doe", "TechPress", 1000, "EPUB")
ebook.copies_sold = 2000
print(f"Royalty for ebook (after GST): {ebook.royalty()}")
