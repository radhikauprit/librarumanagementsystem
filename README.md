import java.util.ArrayList;
import java.util.Scanner;

class User {
    private int id;
    private String name;

    public User(int id, String name){
        this.id = id;
        this.name = name;
    }

    public int getId(){
        return id;
    }

    public String getName(){
        return name;
    }

    public void display(){
        System.out.println("ID: " + id + " | Name: " + name);
    }
}

class Book {
    private String title;
    private int id;
    private boolean isIssued = false;

    public Book(String title, int id){
        this.title = title;
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public int getId(){
        return id;
    }

    public boolean isIssued(){
        return isIssued;
    }

    public void issue(){
        isIssued = true;
    }

    public void returnBook(){
        isIssued = false;
    }

    public void display(){
        System.out.println("ID: " + id + " | Title: " + title + " | Issued: " + (isIssued ? "Yes" : "No"));
    }
}

public class LibrarySystem {
    private ArrayList<User> users = new ArrayList<>();
    private ArrayList<Book> books = new ArrayList<>();
    private Scanner sc = new Scanner(System.in);

    public void start(){
        int choice;
        do {
            System.out.println("\n---- LIBRARY MANAGEMENT SYSTEM ----");
            System.out.println("1. Add User");
            System.out.println("2. Add Book");
            System.out.println("3. View All Books");
            System.out.println("4. View All Users");
            System.out.println("5. Issue Book");
            System.out.println("6. Return Book");
            System.out.println("7. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();
            sc.nextLine(); // consume newline

            switch (choice) {
                case 1: addUser(); break;
                case 2: addBook(); break;
                case 3: viewBooks(); break;
                case 4: viewUsers(); break;
                case 5: issueBook(); break;
                case 6: returnBook(); break;
                case 7: System.out.println("Exiting..."); break;
                default: System.out.println("Invalid choice!");
            }
        } while (choice != 7);
    }

    private void addUser(){
        System.out.print("Enter User ID: ");
        int id = sc.nextInt();
        sc.nextLine();
        System.out.print("Enter Name: ");
        String name = sc.nextLine();

        for (User u : users){
            if (u.getId() == id){
                System.out.println("User already exists.");
                return;
            }
        }

        users.add(new User(id, name));
        System.out.println("User added successfully.");
    }

    private void addBook(){
        System.out.print("Enter Book ID: ");
        int id = sc.nextInt();
        sc.nextLine();
        System.out.print("Enter Book Title: ");
        String title = sc.nextLine();

        for (Book b : books){
            if (b.getId() == id){
                System.out.println("Book already exists.");
                return;
            }
        }

        books.add(new Book(title, id));
        System.out.println("Book added successfully.");
    }

    private void viewBooks(){
        if (books.isEmpty()) {
            System.out.println("No books found.");
            return;
        }

        System.out.println("\n--- Book List ---");
        for (Book b : books) {
            b.display();
        }
    }

    private void viewUsers(){
        if (users.isEmpty()) {
            System.out.println("No users found.");
            return;
        }

        System.out.println("\n--- User List ---");
        for (User u : users) {
            u.display();
        }
    }

    private void issueBook(){
        System.out.print("Enter Book ID to issue: ");
        int bookId = sc.nextInt();

        Book foundBook = null;
        for (Book b : books){
            if (b.getId() == bookId){
                foundBook = b;
                break;
            }
        }

        if (foundBook == null){
            System.out.println("Book not found.");
            return;
        }

        if (foundBook.isIssued()){
            System.out.println("Book is already issued.");
            return;
        }

        foundBook.issue();
        System.out.println("Book issued successfully.");
    }

    private void returnBook(){
        System.out.print("Enter Book ID to return: ");
        int bookId = sc.nextInt();

        Book foundBook = null;
        for (Book b : books){
            if (b.getId() == bookId){
                foundBook = b;
                break;
            }
        }

        if (foundBook == null){
            System.out.println("Book not found.");
            return;
        }

        if (!foundBook.isIssued()){
            System.out.println("Book was not issued.");
            return;
        }

        foundBook.returnBook();
        System.out.println("Book returned successfully.");
    }

    public static void main(String[] args){
        new LibrarySystem().start();
    }
}
