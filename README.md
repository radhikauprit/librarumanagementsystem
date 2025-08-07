# librarumanagementsystem

import java.util.ArrayList;
import java.util.*;
public class user {
    private int id;
    private String name;

    user(int id,String name){
       this.id=id;
       this.name=name;
    }
    
    int getid(){
        return id;
    }

    private String getname(){
        return name;
    }

    void display(){
  System.out.println(" id "+id+" Name "+name);
    }

}

class book{
    private String title;
    private int id;
  private boolean isIssue=false;

  book(String title ,int id){
 this.title=title;
 this.id=id;
  }
   
  public String gettitle() {
      return title;
  }
  public int getid(){
    return id;
  }
  public boolean isIssue(){
    return isIssue;
  }

   public void Issue(){
    isIssue=true;
   } 

   public void returnbook(){
      isIssue=true;
   }
   
   void display(){
    System.out.println("title of book:"+title+"id:"+id+"status:"+isIssue);
   }

}

public class book {
    private String title;
    private int id;
    private boolean isIssued = false;

    public book(String title, int id){
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
import java.util.*;
import java.util.ArrayList.*;

public class library{
ArrayList<user>users=new ArrayList<>();
ArrayList<book>books=new ArrayList<>();
Scanner sc=new Scanner(System.in);

public void start(){
  int choice;
 do{
  System.out.println("--------------LIBRARY MANAGEMENT SYSTEM---------- ");
  System.out.println("1.ADD A USER");
    System.out.println("2.ADD BOOKS");
System.out.println("3.VIEW ALL BOOKS");
    System.out.println("4.VIEW ALL USER");
    System.out.println("5.ISSUE BOOK");
System.out.println("6.RETURN BOOK");  
System.out.println("7.EXITING ");
System.out.println("ENTER YOUR CHOISE (1 to 6)");

choice=sc.nextInt();

switch (choice) {
  case 1:
    adduser();
    break;
    case 2:
    addbook();
    break;
    case 3:
    viewbook();
    break;
    case 4:
    viewauser();
    break;
    case 5:
    issuebook();
    break;
    case 6:
    returnbook();
    break;
    case 7:
    System.out.println("Exiting From System:");
    break;

  default:System.out.println("Invalid Choise Enter Again");
    break;
}
  }while (choice!=7);
}

private void returnbook() {
  // TODO Auto-generated method stub
  throw new UnsupportedOperationException("Unimplemented method 'returnbook'");
}

private void adduser() {
    System.out.println("\n--- Add New User ---");

    System.out.print("Enter User ID (number): ");
    int id = sc.nextInt();
    sc.nextLine(); // consume newline

    System.out.print("Enter User Name: ");
    String name = sc.nextLine();

    // Check for duplicate ID
    for (user u : users) {
        if (u.getid() == id) {
            System.out.println("A user with this ID already exists.");
            return;
        }
    }

    users.add(new user(id, name));
    System.out.println("User added successfully!");
}
  private void addbook(){
    
    System.out.println("\n--- Add New Book ---");

    System.out.print("Enter Book ID (number): ");
    int id = sc.nextInt();
    sc.nextLine(); // consume newline

    System.out.print("Enter Book Title: ");
    String title = sc.nextLine();

    // Check for duplicate ID
    for (book b : books) {
        if (b.getid() == id) {
            System.out.println("A book with this ID already exists.");
            return;
        }
    }

    books.add(new book(title, id));
    System.out.println("Book added successfully!");
}
  private void viewbook(){
    System.out.println("-------VIEW BOOK-----");

    if(books.isEmpty()){
      System.out.println("BOOK ARE NOT PRCENT:");
      return;
    }
    for(book b:books){
      b.display();
    }

  }

  private void viewauser(){
    System.out.println("-----------VIEW USER OF BOOK------------");

    if(users.isEmpty()){
 System.out.println("USER ARE NOT PRESENT");
    }
    for(user u:users){
      u.display();
    }
  }

  private void issuebook(){
    System.out.println("------------ISSUE BOOK---------");
    System.out.println("ENTER A BOOK TITLE");
    String title=sc.nextLine();

    System.out.println("ENTER A ID");
    int id= sc.nextInt();
   
    book foundbook=null;
    for(book b:books){
      if(b.getid()==id){
        foundbook=b;
        return;
      }
    }
    if(foundbook==null){
      System.out.println("it is not found:");
      return;
    }
    if (foundbook.isIssue()) {
        System.out.println("This book is already issued to someone else.");
        return;
    }

    foundbook.Issue();
    System.out.println("Book issued successfully.");
  }
  private void returnBook() {
    System.out.println("\n--- Return a Book ---");

    System.out.print("Enter Book ID to return: ");
    int bookId = sc.nextInt();

    // Find the book
    book foundBook = null;
    for (book b : books) {
        if (b.getid() == bookId) {
            foundBook = b;
            break;
        }
    }

    if (foundBook == null) {
        System.out.println("Book not found.");
        return;
    }

    if (!foundBook.isIssue()) {
        System.out.println("This book is not currently issued.");
        return;
    }

    foundBook.returnbook();
    System.out.println("Book returned successfully.");
}
 public static void main(String[] args){
        new LibrarySystem().start();
    }
}



