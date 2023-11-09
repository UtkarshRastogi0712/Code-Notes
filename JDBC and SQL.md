#Java 

JDBC (Java Database Connectivity) is an API used by Java to communicate with a Database.

### Setup:

```Java
package <package name>;

import java.sql.*;

public class database {
	public static void main(String[] args){
		Connection conn = null;
		try{
			String driverClassName = "Driver Name"; //Database specific driver
			String url = "Database URL";
			String username = "Username";
			String password = "Password";

			Class.forName(driverClassName).getDeclaredConstructor().newInstance();		
			conn = DriverManager.getConnection(url, username, password);
			System.out.println("Connection Established!")
		} catch(Exception ex){
			ex.printStackTrace();
		}
	}
}

```

### Statement:
```Java
Statement stmt = conn.createStatement();

String table = "CREATE TABLE AIRLINE(id INT NOT NULL PRIMARY KEY, name CHAR(50), source CHAR(50), destination CHAR(50), age INT, date DATE);";

stmt.executeUpdate(table);
System.out.println("Table create");
```

### Prepared Statement:
```Java
String passenger = "INSERT INTO AIRLINE VALUES (?,?,?,?,?,?)";
PreparedStatement pstmt = conn.prepareStatement(passenger);

System.out.println("Enter number of passengers");
int passengerCount = sc.nextInt();
sc.nextLine();
for(int i = 0;i<passengerCount;i++){
    pstmt.setInt(1,i+1);

    System.out.println("Enter name:");
    String name = sc.nextLine();
    pstmt.setString(2,name);

    System.out.println("Enter source:");
    String from = sc.nextLine();
    pstmt.setString(3,from);

    System.out.println("Enter destination:");
    String to = sc.nextLine();
    pstmt.setString(4,to);

    System.out.println("Enter age:");
    int age = sc.nextInt();
    sc.nextLine();
    pstmt.setInt(5,age);

    System.out.println("Enter date:");
    String date = sc.nextLine();
    pstmt.setString(6,date);

    pstmt.executeUpdate();
}
System.out.println("Values inserted into airline");
```

### Result set:
```Java
String select = "SELECT * FROM AIRLINE;";
Statement selstmt = conn.createStatement();
ResultSet rs = selstmt.executeQuery(select);
while(rs.next()){
    System.out.println("Details of passenger "+rs.getInt(1));
    System.out.println("Name: "+rs.getString(2));
    System.out.println("Source: "+rs.getString(3));
	System.out.println("Destination: "+rs.getString(4));
	System.out.println("Age: "+rs.getInt(5));
	System.out.println("Date: "+rs.getString(6));
}
```

SQL cheatsheet : [[SQL]]