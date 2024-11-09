public class Book {
    private String title;
    private String author;
    private String isbn;
    private boolean isAvailable;

    // Constructor
    public Book(String title, String author, String isbn) {
        this.title = title;
        this.author = author;
        this.isbn = isbn;
        this.isAvailable = true;
    }

    // Getters and Setters
    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }

    public String getIsbn() {
        return isbn;
    }

    public boolean isAvailable() {
        return isAvailable;
    }

    public void setAvailable(boolean available) {
        isAvailable = available;
    }

    @Override
    public String toString() {
        return "Title: " + title + ", Author: " + author + ", ISBN: " + isbn + ", Available: " + isAvailable;
    }
}
2. Define the Member Class
This class will represent library members.

java
Copy code
public class Member {
    private String name;
    private int memberId;
    private int borrowedBooks;

    // Constructor
    public Member(String name, int memberId) {
        this.name = name;
        this.memberId = memberId;
        this.borrowedBooks = 0;
    }

    // Getters and Setters
    public String getName() {
        return name;
    }

    public int getMemberId() {
        return memberId;
    }

    public int getBorrowedBooks() {
        return borrowedBooks;
    }

    public void borrowBook() {
        borrowedBooks++;
    }

    public void returnBook() {
        if (borrowedBooks > 0) {
            borrowedBooks--;
        }
    }

    @Override
    public String toString() {
        return "Member Name: " + name + ", ID: " + memberId + ", Borrowed Books: " + borrowedBooks;
    }
}
3. Define the Library Class
This class manages the book inventory and members.

java
Copy code
import java.util.ArrayList;

public class Library {
    private ArrayList<Book> books;
    private ArrayList<Member> members;

    // Constructor
    public Library() {
        books = new ArrayList<>();
        members = new ArrayList<>();
    }

    // Add a new book to the library
    public void addBook(Book book) {
        books.add(book);
    }

    // Register a new member
    public void registerMember(Member member) {
        members.add(member);
    }

    // Borrow a book
    public boolean borrowBook(String isbn, int memberId) {
        for (Book book : books) {
            if (book.getIsbn().equals(isbn) && book.isAvailable()) {
                for (Member member : members) {
                    if (member.getMemberId() == memberId) {
                        book.setAvailable(false);
                        member.borrowBook();
                        System.out.println("Book borrowed successfully.");
                        return true;
                    }
                }
            }
        }
        System.out.println("Book or member not found, or book not available.");
        return false;
    }

    // Return a book
    public boolean returnBook(String isbn, int memberId) {
        for (Book book : books) {
            if (book.getIsbn().equals(isbn) && !book.isAvailable()) {
                for (Member member : members) {
                    if (member.getMemberId() == memberId) {
                        book.setAvailable(true);
                        member.returnBook();
                        System.out.println("Book returned successfully.");
                        return true;
                    }
                }
            }
        }
        System.out.println("Book or member not found, or book was not borrowed.");
        return false;
    }

    // Display all books
    public void displayBooks() {
        for (Book book : books) {
            System.out.println(book);
        }
    }

    // Display all members
    public void displayMembers() {
        for (Member member : members) {
            System.out.println(member);
        }
    }
}
4. Create a Main Class for Testing
This is where the library system is initialized and tested.

java
Copy code
public class LibraryManagementSystem {
    public static void main(String[] args) {
        Library library = new Library();

        // Adding books
        library.addBook(new Book("The Great Gatsby", "F. Scott Fitzgerald", "123456789"));
        library.addBook(new Book("1984", "George Orwell", "987654321"));
        
        // Registering members
        library.registerMember(new Member("Alice", 1));
        library.registerMember(new Member("Bob", 2));

        // Display books and members
        System.out.println("Library books:");
        library.displayBooks();

        System.out.println("\nLibrary members:");
        library.displayMembers();

        // Borrowing a book
        library.borrowBook("123456789", 1);

        // Display books after borrowing
        System.out.println("\nLibrary books after borrowing:");
        library.displayBooks();

        // Returning a book
        library.returnBook("123456789", 1);

        // Display books after returning
        System.out.println("\nLibrary books after returning:");
        library.displayBooks();
    }
}
