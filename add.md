
import java.sql.*;

public class Demo {
    public static void main(String arg[])
    {
        try {
            // below two lines are used for connectivity.
            Connection connection =  DriverManager.getConnection(
                    "jdbc:mysql://localhost:3306/employee_db?characterEncoding=utf8",
                    "root", "123456");


            Statement statement;
            statement = connection.createStatement();
            ResultSet resultSet;
            resultSet = statement.executeQuery(
                    "select * from emp_proj");


            while (resultSet.next()) {
                System.out.println(resultSet.getInt(1)+ " "+ resultSet.getString(2)+ " "+ resultSet.getString(3));
            }
            resultSet.close();
            statement.close();
            connection.close();
        }
        catch (Exception exception) {
            System.out.println(exception);
        }
    }
}
