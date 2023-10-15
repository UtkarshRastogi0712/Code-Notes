#Java 

JDBC (Java Database Connectivity) is an API used by Java to communicate with a Database.

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