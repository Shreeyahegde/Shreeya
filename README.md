Slip1:
1. Write a Java program to display all the alphabets between ‘A’ to ‘Z’ after every 2 seconds.
public class S1 extends Thread
{
char c;
public void run()
{
for(c = 'A'; c<='Z';c++)
{
System.out.println(""+c);
try

{
Thread.sleep(3000);
}
catch(Exception e)
{
e.printStackTrace();
}
}
}
public static void main(String args[])
{
S1 t = new S1();
t.start();
}
}

2. Write a Java program to accept the details of Employee (Eno, EName, Designation, Salary) from a user and store it into the database. (Use Swing)
import java.sql.*;
import java.awt.*;
import javax.swing.*;
import java.awt.event.*;

class S1_2 extends JFrame implements ActionListener {
    JLabel l1, l2, l3, l4;
    JTextField txt1, txt2, txt3, txt4;
    JButton submit, clear;

    S1_2() {
        l1 = new JLabel("Employee no");
        l2 = new JLabel("Name");
        l3 = new JLabel("Designation");
        l4 = new JLabel("Salary ");
        txt1 = new JTextField(20);
        txt2 = new JTextField(20);
        txt3 = new JTextField(20);
        txt4 = new JTextField(20);
        submit = new JButton("submit");
        submit.addActionListener(this);
        clear = new JButton("Clear");
        clear.addActionListener(this);

        setLayout(new GridLayout(5, 2));
        add(l1);
        add(txt1);
        add(l2);
        add(txt2);
        add(l3);
        add(txt3);
        add(l4);
        add(txt4);
        add(submit);
        add(clear);
        setTitle("Employee information");
        setVisible(true);
        setSize(400, 400);
    }

    public void actionPerformed(ActionEvent ae) {
        if (ae.getSource() == submit) {
            try {
                Class.forName("org.postgresql.Driver");
                Connection c = DriverManager.getConnection("jdbc:postgresql://localhost:5432/ty", "postgres", "123");
                Statement s = c.createStatement();
                String query = "INSERT INTO emp VALUES (" + txt1.getText() + ", '" + txt2.getText() + "', '" + txt3.getText() + "', " + txt4.getText() + ")";
                s.executeUpdate(query);
           
                JOptionPane.showMessageDialog(null, "Record inserted successfully....");
            } catch (Exception er) {
                er.printStackTrace();
                JOptionPane.showMessageDialog(null, "Error: " + er.getMessage());
            }
        }
        if (ae.getSource() == clear) {
            txt1.setText("");
            txt2.setText("");
            txt3.setText("");
            txt4.setText("");
        }
    }

    public static void main(String args[]) {
        new S1_2();
    }
}
// To run:
student@student-ThinkCentre-E73:$ export CLASSPATH=$CLASSPATH:/home/student/Downloads/postgresql-42.7.1.jar
student@student-ThinkCentre-E73:$ javac S1_2.java
student@student-ThinkCentre-E73:$ java S1_2
Slip2:
Write a java program to read ‘N’ names of your friends, store it into HashSet and
display them in ascending order.
import java.util.*;
public class Slip2_1
{
public static void main(String args[])
{
Scanner sc=new Scanner(System.in);
System.out.println("Enetr the number of the friends:");
int n=sc.nextInt();
HashSet<String> f=new HashSet<String>();
for(int i=0;i<n;i++)
{
System.out.println("Enetr name"+i+":");
String name=sc.next();
f.add(name);
}
System.out.println("Friend List:"+f);
TreeSet<String> t=new TreeSet<String>(f);
System.out.println("Friend List in ascending order:"+t);

}
}

2. Design a servlet that provides information about a HTTP request from a client, such as
IP-Address and browser type. The servlet also provides information about the server on
which the servlet is running, such as the operating system type, and the names of
currently loaded servlets.
//Slip2_2.java
import java.io.*;
        import javax.servlet.*;
        import javax.servlet.http.*;
public class Slip2_2 extends HttpServlet implements Servlet
{
    protected void doGet(HttpServletRequest req,HttpServletResponse res)throws IOException,ServletException
    {
        res.setContentType("text/html");
        PrintWriter pw=res.getWriter();
        pw.println("<html><body><h2>Information about Http Request</h2>");
        pw.println("<br>Server Name: "+req.getServerName());
        pw.println("<br>Server Port: "+req.getServerPort());
        pw.println("<br>Ip Address: "+req.getRemoteAddr());
        pw.println("<br>Client Browser: "+req.getHeader("User-Agent"));
        pw.println("</body></html>");
        pw.close();
    }
}



//Web.xml
    <web-app>  
      
    <servlet>  
    <servlet-name>Slip</servlet-name>  
    <servlet-class>Slip2_2</servlet-class>  
    </servlet>  
      
    <servlet-mapping>  
    <servlet-name>Slip</servlet-name>  
    <url-pattern>/s</url-pattern>  
    </servlet-mapping>  
      
    </web-app>  

Slip3:
Write a JSP program to display the details of Patient (PNo, PName, Address, age,
disease) in tabular form on browser.
//Slip3_1.jsp
<html> 
<body> 
<h1>Patient information</h1> 
<table border="1"> 
<tr> <th>PNo</th> <th>PName</th> <th>Address</th> <th>age</th> <th>disease</th> </tr> <tr> 
<td>1</td> <td>John</td> <td>xyz</td> <td>Nashik</td> <td>kovid</td> </<tr> 
<tr> <td>2</td> <td>Brock</td> <td>Pune</td> <td>48</td> <td>canser</td> </<tr>
<tr> <td>3</td> <td>Rohan</td> <td>Nashik</td> <td>48</td> <td>canser</td> </<tr>
 </table> 
 </body> 
 </html>

2. Write a Java program to create LinkedList of String objects and perform the following:
i. Add element at the end of the list
ii. Delete first element of the list
iii. Display the contents of list in reverse order
import java.util.*;
public class Slip3_2 {
    public static void main(String[] args)
    {
       
        LinkedList<String> L = new LinkedList<String>();
        
        L.add("Red");
        L.add("Green");
        L.add("Yello");
        System.out.println("Elements in the list: " + L);
        L.addLast("Blue");
        System.out.println("Elements after adding element at last: " + L);
        L.removeFirst();
         System.out.println("Elements after deleting first element: " + L);
         ListIterator li=L.listIterator();
         while(li.hasNext())
         li.next();
          System.out.println("Elements in reverse order: ");
         while(li.hasPrevious())
            System.out.print("\t"+ li.previous());
    
    
}
}

Slip4:
1. Write a Java program using Runnable interface to blink Text on the JFrame (Use
Swing)
import java.awt.*;
import javax.swing.*;
import java.awt.event.*;
public class Slip4_1 extends JFrame implements Runnable
{
            Thread t;
            JLabel l1;
            int f;
            public Slip4_1()
            {
                        t=new Thread(this);
                        t.start();
                        setLayout(null);
                        l1=new JLabel("Hello JAVA");
                        l1.setBounds(100,100,100,40);
                        add(l1);
                        setSize(300,300);
                        setVisible(true);
                        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);   
                        f=0;
            }
            public void run()
            {
                        try
                        {
                                    if(f==0)
                                    {
                                                t.sleep(200);
                                                l1.setText("");
                                                f=1;
                                    }
                                    if(f==1)
                                    {
                                                t.sleep(200);
                                                l1.setText("Hello Java");
                                                f=0;
                                    }
                        }catch(Exception e)
                        {
                                    System.out.println(e);
                        }
                        run();
            }
            public static void main(String args[])
            {
                        new Slip4_1();
            }
}

2. Write a Java program to store city names and their STD codes using an appropriate
collection and perform following operations:
i. Add a new city and its code (No duplicates)
ii. Remove a city from the collection
iii. Search for a city name and display the code
import java.util.*;
 
public class Slip4_2 
{
    public static void main(String[] args)
    {
        Hashtable<String, Integer> hashtable = new Hashtable<>();
 	Scanner sc=new Scanner(System.in);
 	int ch;
 	do
 	{
 	System.out.println("1.Add a new city and its code\n2. Remove a city from the collection\n3. Search for a city name and display the code\n4.Exit");
 	ch=sc.nextInt();
 	switch(ch)
 	{
 	case 1:
 	System.out.println("Enter the city name and code:");
 	String city=sc.next();
 	int code=sc.nextInt();
        hashtable.put(city,code);
        System.out.println("List:"+hashtable);
        break;
        case 2:
 	System.out.println("Enter the city name to delete:");
 	String c=sc.next();
  	hashtable.remove(c);
  	 System.out.println("List:"+hashtable);
  	break;
  	case 3:
  	System.out.print("Enter city name to search: ");
        String cityName = scanner.next();
        String stdCode = hashtable.get(cityName);
        if (stdCode == null) {
            System.out.println("City not found in the collection.");
        } else {
            System.out.println("STD code for " + cityName + ": " + stdCode);
            }
            break;
  	case 4: System.exit(0);
  	}
  	}while(ch!=4);
  }
 }
  
Slip7:
1.	Write a java program that implements a multi-thread application that has three threads. First thread generates random integer number after every one second, if the number is even; second thread computes the square of that number and prints it. If the number is odd, the third thread computes the cube of that number and prints it.
import java.util.*;
class Square extends Thread
{
int x;
Square(int n)
{
x = n;
}
public void run()
{
int sqr = x * x;
System.out.println("Square of " + x + " = " + sqr );
}
}

class Cube extends Thread
{
int x;
Cube(int n)
{
x = n;
}
public void run()
{
int cub = x * x * x;
System.out.println("Cube of " + x + " = " + cub );
}
}

class Number extends Thread
{
public void run()
{
Random random = new Random();
for(int i =0; i<10; i++)
{
int rd = random.nextInt(100);
if(rd%2==0)
{
Square s = new Square(rd);
s.start();
}
else
{
Cube c = new Cube(rd);
c.start();
}
try {
Thread.sleep(1000);
} catch (InterruptedException ex) {
System.out.println(ex);
}
}
}
}
public class Slip7_1
 {
public static void main(String args[])
{
Number n = new Number();
n.start();
}
}

Slip7_2	
2. Write a java program for the following:
i. To create a Product (Pid, Pname, Price) table.
ii. Insert at least five records into the Product table.
iii. Display all the records from a Product table.
Assume Database is already created.
import java.sql.*;
import java.util.*;
public class Slip7_2 {
    public static void main (String args[]) 
    {
        Connection c = null;
        try {
            Class.forName("org.postgresql.Driver");
            Scanner sc = new Scanner(System.in);
            c = DriverManager.getConnection("jdbc:postgresql://localhost:5432/ty", "postgres", "123");
            
            Statement s = c.createStatement();
            s.executeUpdate("create table product(pid int, pname varchar(20), price int)");

            System.out.println("Enter how many records?");
            int n = sc.nextInt();
            for (int i = 0; i < n; i++) 
            {
                System.out.println("Enter product information: pid, product name, and price");
                int p = sc.nextInt();
                String name = sc.next();
                int pri = sc.nextInt();
                String sql = "insert into product values(" + p + ",'" + name + "'," + pri + ")";
                int y = s.executeUpdate(sql);
                if (y > 0)
                    System.out.println("Record inserted successfully...");
            }

            System.out.println("......Product information.......");
            ResultSet rs = s.executeQuery("select * from product");
            while (rs.next()) {
                System.out.println(rs.getInt(1) + "\t" + rs.getString(2) + "\t" + rs.getInt(3));
            }
        } catch (Exception e) 
        {
            e.printStackTrace();
            System.exit(0);
        } 
    }
}
  	
Slip 8:
1. Write a java program to define a thread for printing text on output screen for ‘n’
number of times. Create 3 threads and run them. Pass the text ‘n’ parameters to the
thread constructor.
Example:
i. First thread prints “COVID19” 10 times.
ii. Second thread prints “LOCKDOWN2020” 20 times
iii. Third thread prints “VACCINATED2021” 30 times
class TextPrinter extends Thread
 {

    private String text;
    private int n;

    public TextPrinter(String text, int n) {
        this.text = text;
        this.n = n;
    }

    public void run()
     {
        for (int i = 0; i < n; i++) 
        {
            System.out.println(text);
        }
    }
}

public class Slip8_1
 {
    public static void main(String[] args) {
        Thread t1 = new TextPrinter("COVID19", 10);
        Thread t2 = new TextPrinter("LOCKDOWN2020", 20);
        Thread t3 = new TextPrinter("VACCINATED2021", 30);

        t1.start();
        t2.start();
        t3.start();
    }
}

2. Write a JSP program to check whether a given number is prime or not. Display the result
in red color.
Slip8_2.html
<html>
<body>
    <h2>Prime Number Checker</h2>
    <form method="post" action="Slip8_2.jsp">
        Enter a number: <input type="text" name="number">
        <input type="submit" value="Check">
    </form>
    </body>
    </html>
Slip8_2.jsp
    <%
    int num =Integer.parseInt(request.getParameter("number"));
    int flag=0;
       for(int i=2;i<num/2;i++)
       {
       if(num%i==0)
       {
       flag=1;
       break;
       }
       }
       if(flag==1)
       {
       %>
<h2 style="color:red; font-size:18px;"> <%= num %> is not a prime</h2>
<%
}
else
{
 %>
<h2 style="color:red; font-size:18px;"> <%= num %> is a prime</h2>
<%
}
%>
</body>
</html>

Slip12
1. Write a JSP program to check whether given number is Perfect or not. (Use Include
directive).
//Slip12_1.html
<html>
<body>
    <h2>Perfect Number Checker</h2>
    <form method="post" action="Slip12_1.jsp">
        Enter a number: <input type="text" name="number">
        <input type="submit" value="Check">
    </form>
    </body>
    </html>
//Slip12_2.jsp

    <%
    int num =Integer.parseInt(request.getParameter("number"));
  int a=num, sum=0;
       for(int i=1;i<num;i++)
       {
       sum=sum+i;
       }
       if(sum==a)
       {
       %>
<h2 style="color:red; font-size:18px;"> <%= num %> is a perfect number</h2>
<%
}
else
{
 %>
<h2 style="color:red; font-size:18px;"> <%= num %> is not a perfect number</h2>
<%
}
%>
</body>
</html>

Slip13:
1. Write a Java program to display information about the database and list all the tables in
the database. (Use DatabaseMetaData).
import java.sql.*;

public class Slip13_1
{
   public static void main(String args[]) 
   {
      Connection c = null;
      try {
         Class.forName("org.postgresql.Driver");
         c = DriverManager.getConnection("jdbc:postgresql://localhost:5432/ty","postgres", "123");
          DatabaseMetaData  md = c.getMetaData();
            System.out.println("Database Product Name: " + md.getDatabaseProductName());
            System.out.println("Database Product Version: " + md.getDatabaseProductVersion());
            System.out.println("Driver Name: " + md.getDriverName());
            System.out.println("Driver Version: " + md.getDriverVersion());
            System.out.println();

            // List all tables in the database
            ResultSet tables = md.getTables(null, null, "%", new String[]{"TABLE"});
            System.out.println("Tables in the database:");
            while (tables.next()) {
                String tableName = tables.getString("TABLE_NAME");
                System.out.println(tableName);
            }
      } 
      catch (Exception e) 
      {
         e.printStackTrace();
       System.exit(0);
      }
      
   }
}


2. Write a Java program to show lifecycle (creation, sleep, and dead) of a thread. Program
should print randomly the name of thread and value of sleep time. The name of the
thread should be hard coded through constructor. The sleep time of a thread will be a
random integer in the range 0 to 4999.
import java.util.*;

class MyThread extends Thread 
{
    public MyThread(String name)
     {
     
        super(name);
    }
    public void run() 
    {
        Random random = new Random();
        int sleepTime = random.nextInt(5000);
        System.out.println("Thread " + getName() + " sleeping for " + sleepTime + " milliseconds.");
        
        try
         {
           
            Thread.sleep(sleepTime);
        } 
        catch (InterruptedException e) 
        {
            e.printStackTrace();
        }
        System.out.println("Thread " + getName() + " has completed its execution.");
    }
}
public class Slip13_2
 {
    public static void main(String[] args) 
    {
        MyThread m = new MyThread("MyThread");
        m.start();
    }
}








Slip15:
1. Write a java program to display name and priority of a Thread.
public class Slip15_1
 {
    public static void main(String[] args)
     {
        Thread thread = Thread.currentThread();
        System.out.println("Thread Name: " + thread.getName());
        System.out.println("Thread Priority: " + thread.getPriority());
    }
}

2. Write a SERVLET program which counts how many times a user has visited a web
page. If user is visiting the page for the first time, display a welcome message. If the
user is revisiting the page, display the number of times visited. (Use Cookie)
//Slip15_2.java 
import java.io.*;
 import javax.servlet.*;
 import javax.servlet.http.*;
public class Slip15_2 extends HttpServlet
{
    static int i=1;
    public void doGet(HttpServletRequest request,HttpServletResponse response)throws IOException,ServletException
    {
        response.setContentType("text/html");
        PrintWriter out=response.getWriter();
        String k=String.valueOf(i);
        Cookie c=new Cookie("visit",k);
        response.addCookie(c);
        int j=Integer.parseInt(c.getValue());
        if(j==1)
        {
            out.println("Welcome to web page ");
        }
        else        {
            out.println("You are visited at "+i+" times");
        }
        i++;
    }
}

//web.xml
<web-app>  
      
    <servlet>  
    <servlet-name>Slip</servlet-name>  
    <servlet-class>Slip15_2</servlet-class>  
    </servlet>  
      
    <servlet-mapping>  
    <servlet-name>Slip</servlet-name>  
    <url-pattern>/s</url-pattern>  
    </servlet-mapping> 
    </web-app>  

Slip16
1. Write a java program to create a TreeSet, add some colors (String) and print out the
content of TreeSet in ascending order.
import java.util.*;

public class Slip16_1
 {
    public static void main(String[] args) 
    {
        
        TreeSet<String> colors = new TreeSet<>();
        colors.add("Red");
        colors.add("Green");
        colors.add("Blue");
        colors.add("Yellow");
        colors.add("Orange");
        System.out.println("Colors in ascending order:"+colors);
        
        }
    
}

2. Write a Java program to accept the details of Teacher (TNo, TName, Subject). Insert at
least 5 Records into Teacher Table and display the details of Teacher who is teaching
“JAVA” Subject. (Use PreparedStatement Interface)

import java.sql.*;
import java.util.*;
public class Slip16_2
 {
    public static void main(String[] args) 
    {
        Connection c = null;
        PreparedStatement pstmt = null;
        Statement stmt = null;
        Scanner sc=new Scanner(System.in);
        try {
           Class.forName("org.postgresql.Driver");
            c = DriverManager.getConnection("jdbc:postgresql://localhost:5432/ty", "postgres", "123");
            String sql = "INSERT INTO teacher VALUES (?, ?, ?)";
            pstmt = c.prepareStatement(sql);
            for (int i = 1; i <= 5; i++) 
            {
                pstmt.setInt(1, i); 
                System.out.println("enter teacher name and subject:");
                String t=sc.next();
                String sub=sc.next();
                pstmt.setString(2,t);
                pstmt.setString(3,sub);
                pstmt.executeUpdate();
            }
            System.out.println("Teachers teaching JAVA subject:");
            stmt = c.createStatement();
            String s = "SELECT * FROM teacher WHERE subject = 'java'";
            ResultSet rs = stmt.executeQuery(s);
            while (rs.next())
             {
                int tNo = rs.getInt("TNo");
                String tName = rs.getString("TName");
                String subject = rs.getString("Subject");
                System.out.println("Teacher Number: " + tNo + ", Teacher Name: " + tName + ", Subject: " + subject);
            }

   
        } catch (Exception se) {
            se.printStackTrace();
       
        }
    }
}
Slip17
1. Write a java program to accept ‘N’ integers from a user. Store and display integers in
sorted order having proper collection class. The collection should not accept duplicate
elements.
import java.util.TreeSet; 
import java.util.Scanner;
public class B1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        TreeSet<Object> ts = new TreeSet<>();

        System.out.println("Enter how many Numbers: ");
        int n = sc.nextInt();

        System.out.println("Enter the " + n + " Numbers: ");
        for (int i = 0; i < n; i++) {
            int num = sc.nextInt();
            ts.add(num);
        }
        System.out.println("Numbers in Sorted Order and without Duplication :" + ts);
        sc.close();
    }
}

2. Write a java program using Multithreading to display the number’s between 1 to 100
continuously in a JTextField by clicking on JButton. (Use Runnable Interface &
Swing).
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
public class MultiThread extends JFrame implements ActionListener
{
    Container cc;
    JButton b1,b2;
    JTextField t1;
    MultiThread()
    {
        setVisible(true);
        setSize(1024,768);
        cc=getContentPane();
        setLayout(null);
        t1=new JTextField(500);
        cc.add(t1);
        t1.setBounds(10,10,1000,30);
        b1=new JButton("start");
        cc.add(b1);
        b1.setBounds(20,50,100,40);
        b1.addActionListener(this);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }
    public void actionPerformed(ActionEvent e)
    {
        if(e.getSource()==b1)
        {
            new Mythread();
        }
    }
    class Mythread extends Thread
    {
        Mythread()
        {
        start();
        }
        public void run()
        {
            for(int i=1;i<=100;i++)
            {
                try                {
                    Thread.sleep(1000);
                }
                catch (InterruptedException e) {
                }
                t1.setText(t1.getText()+""+i+"\n");
//System.out.println()            }
        }
    }
    public static void main(String arg[])
    {
        new MultiThread().show();
    }
}


Slip23:
1.	Write a java program using Multithreading to accept a String from a user and display each vowel from a String after every 3 seconds.
import java.util.*;
class vowel extends Thread
 {
    String str;

    vowel(String str) 
    {
        this.str = str;
    }

    public void run()
     {
     try
     {
        for (int i = 0; i < str.length(); i++) 
        {
            char ch = str.charAt(i);
            if (ch == 'A' || ch == 'E' || ch == 'I' || ch == 'O' || ch == 'U' || ch == 'a' || ch == 'e' || ch == 'i' || ch == 'O' || ch == 'u') 
            {
                System.out.println(ch);
                 Thread.sleep(3000); // Sleep for 3 seconds
             }
            }
        }
        catch (InterruptedException e) {
                    e.printStackTrace();}
    }

    
}

public class Slip23_1
 {
    public static void main(String[] args)
     {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a string: ");
        String s = sc.next();
        vowel v = new vowel(s);
        v.start();
    }
}

2.	Write a java program to accept ‘N’ student names through command line, store them
into the appropriate Collection and display them by using Iterator and ListIterator
interface.
import java.util.*;
public class Slip23_2
 {
    public static void main(String[] args) 
    {
        List<String> L = new ArrayList<>();

        for (int i=0;i<args.length;i++) 
        {
           L.add(args[i]);
        }

        System.out.println("Student names using Iterator:");
        Iterator<String> itr = L.iterator();
        while (itr.hasNext())
        {
            System.out.println(itr.next());
        }

        System.out.println("\nStudent names using ListIterator:");
        ListIterator<String> litr = L.listIterator();
        while (litr.hasNext()) 
        {
            System.out.println(litr.next());
        }
    }
}
// To run: 
sujata@sujata-virtual-machine:~/Java-II$ javac Slip23_2.java
sujata@sujata-virtual-machine:~/Java-II$ java Slip23_2 Ram Sam Riya Siya
Student names using Iterator:
Ram
Sam
Riya
Siya

Student names using ListIterator:
Ram
Sam
Riya
Siya

Slip25
1.	Write a JSP program to accept Name and Age of Voter and check whether he is
eligible for voting or not.
//Slip25_1.html
<html>
<body>
<form action="Slip25_1.jsp" method="post">
Name : <input type="text" name="name">

Age : <input type="text" name="age">

<input type="submit" value="Check">
</form>
</body>
</html>

//Slip25_1.jsp
<%
String name = request.getParameter("name");
int age = Integer.parseInt(request.getParameter("age"));
if(age >=18)
{
out.println(name + "\nAllowed to vote");
}
else
{
out.println(name + "\nNot allowed to vote");
}
%>

 2. Write a Java Program for the following: Assume database is already created.
//Slip25_2.java
import java.sql.*;
import java.awt.*;
import javax.swing.*;
import java.awt.event.*;

public class Slip25_2 extends JFrame implements ActionListener 
{

    Connection c = null;
    JLabel l, l1;
    JTextField t1;
    JButton b1, b2, b3;

    Slip25_2() 
    {
        l = new JLabel("Enter your DDL Query here:");
        l1 = new JLabel();
        t1 = new JTextField(50);
        b1 = new JButton("Create");
        b2 = new JButton("Alter");
        b3 = new JButton("Drop");
        b1.addActionListener(this);
        b2.addActionListener(this);
        b3.addActionListener(this);
        setLayout(new GridLayout(2, 3, 10, 20));
        setSize(700, 200);
        setVisible(true);
        add(l);
        add(l1);
        add(t1);
        add(b1);
        add(b2);
        add(b3);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }

    public void actionPerformed(ActionEvent e) {
        try {
            Class.forName("org.postgresql.Driver");
            c = DriverManager.getConnection("jdbc:postgresql://localhost:5432/ty", "postgres", "123");
            String q = t1.getText();
            Statement s = c.createStatement();
            if (e.getSource() == b1) 
            {
                s.execute(q);
                JOptionPane.showMessageDialog(null, "Table is created.");
            } 
            else if (e.getSource() == b2) 
            {
                s.execute(q);
                JOptionPane.showMessageDialog(null, "Table is altered.");
            } 
            else if (e.getSource() == b3) 
            {
                s.execute(q);
                JOptionPane.showMessageDialog(null, "Table is dropped.");
            }
            c.close();
        } 
        catch (Exception ex) 
        {
            ex.printStackTrace();
            System.exit(0);
        }
    }

    public static void main(String args[]) 
    {
        new Slip25_2();
    }
}

Slip26:
1. Write a Java program to delete the details of given employee (ENo EName Salary).
Accept employee ID through command line. (Use PreparedStatement Interface)
import java.sql.*;
// create table in postgres
postgres=# \c ty
You are now connected to database "ty" as user "postgres".
ty=# create table employee(eno int,ename varchar(20),salary int);
CREATE TABLE
ty=# insert into employee values(101,'Sujata',2324442);
INSERT 0 1

//Slip26_1.java
public class Slip26_1 {
   public static void main(String args[])
    {
 
      try {
          int eid=Integer.parseInt(args[0]);
         Class.forName("org.postgresql.Driver");
         Connection c =DriverManager.getConnection("jdbc:postgresql://localhost:5432/ty","postgres", "123");
            PreparedStatement p = c.prepareStatement("DELETE FROM employee WHERE ENo = ?"); 
             p.setInt(1, eid);
             int r=p.executeUpdate();
             if(r>0)
             System.out.println("Record deleted successfully....");
            
      } 
      catch (Exception e) 
      {
         e.printStackTrace();
         System.exit(0);
      }
     
   }
}

To run: sujata@sujata-virtual-machine:~/Java-II$ javac Slip26_1.java
sujata@sujata-virtual-machine:~/Java-II$ java Slip26_1 101      <-command line arguments
Record deleted successfully....

2. Write a JSP program to calculate sum of first and last digit of a given number. Display
sum in Red Color with font size 18.
//Slip26_2.html
<html>
<body>
<form method=post action="Slip26_2.jsp">
Enter Any Number : <input type="text" name="num">
<input type="submit" value="Display">
</form>
</body>
</html>

//Slip26_2.jsp
<%! int n,rem,r; %>
<% n=Integer.parseInt(request.getParameter("num"));
if(n<10)
{
%><h2 style="color:red; font-size:18px;">Sum of First and Last Digit: <%= n %></h2>
<%
}
else
{
rem=n%10;
do
{
r=n%10;
n=n/10;
}while(n>0);
n=rem+r;
%>
<h2 style="color:red; font-size:18px;">Sum of First and Last Digit: <%= n %></h2>
<%
}
%>


Slip28:
1.	Write a JSP script to accept a String from a user and display it in reverse order.
//Slip28_1.jsp
<html>
<body>
<form method="post">
Enetr String:<input type="text" name="str">
<input type="submit" value="Reverse">
</form>
<br>
<%
String s=request.getParameter("str");
if(s!=null && !s.isEmpty())
{
String rev=new StringBuilder(s).reverse().toString();
out.println("Original string:"+s+"<br>");
out.println("Reverse string:"+rev);
}
%>
</body>
</html>

2.	Write a java program to display name of currently executing Thread in multithreading.
public class Slip28_2
{
public static void main(String args[])
{
Thread t=Thread.currentThread();
System.out.println("Thread Name is:"+t.getName());
}
}

Slip29:
1. Write a Java program to display information about all columns in the DONAR table
using ResultSetMetaData.
import java.sql.*;

public class Slip29_1
 {
   public static void main(String args[]) 
   {
      Connection c = null;
      try {
         Class.forName("org.postgresql.Driver");
         c = DriverManager.getConnection("jdbc:postgresql://localhost:5432/ty","postgres", "123");
         Statement s= c.createStatement();
         ResultSet rs = s.executeQuery("select * from donar");
         ResultSetMetaData md = rs.getMetaData();
                int columnCount = md.getColumnCount();
         System.out.println("Columns in the donar table:");
                for (int i = 1; i <= columnCount; i++)
                 {
                  
                    System.out.println("Column name: " + md.getColumnName(i));
                    System.out.println("Column type: " + md.getColumnTypeName(i));
                    System.out.println("Column size: " + md.getColumnDisplaySize(i));
                    System.out.println("--------------------------");
                } 
      }
      catch (Exception e) {
         e.printStackTrace();
      }
     
   }
}

2. Write a Java program to create LinkedList of integer objects and perform the following:
i. Add element at first position
ii. Delete last element
iii. Display the size of link list

import java.util.*;
 
public class Slip29_2 {
    public static void main(String[] args)
    {
       
        LinkedList<String> L = new LinkedList<String>();
        
        L.add("Red");
        L.add("Green");
        L.add("Yellow");
        System.out.println("Elements in the list: " + L);
        L.addFirst("Blue");
        System.out.println("Elements after adding element at first: " + L);
        L.removeLast();
         System.out.println("Elements after deleting last element: " + L);
          System.out.println("Size of linkedlist: "+L.size());
        
    }
 
 
    
}
