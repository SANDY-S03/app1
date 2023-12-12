import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class PostgreSQLExample {

    // JDBC URL, username, and password of PostgreSQL server
    private static final String JDBC_URL = "jdbc:postgresql://your_host:your_port/your_database";
    private static final String USERNAME = "your_username";
    private static final String PASSWORD = "your_password";

    public static void main(String[] args) {
        Connection connection = null;

        try {
            // Register the PostgreSQL driver
            Class.forName("org.postgresql.Driver");

            // Establish a connection
            connection = DriverManager.getConnection(JDBC_URL, USERNAME, PASSWORD);

            // Perform database operations
            executeDatabaseOperations(connection);

        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        } finally {
            // Close the connection in the finally block to ensure it's always closed
            if (connection != null) {
                try {
                    connection.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    private static void executeDatabaseOperations(Connection connection) throws SQLException {
        // Example: Select data from a table
        String selectQuery = "SELECT * FROM your_table";
        try (PreparedStatement preparedStatement = connection.prepareStatement(selectQuery)) {
            ResultSet resultSet = preparedStatement.executeQuery();

            while (resultSet.next()) {
                // Retrieve data from the result set
                int column1Value = resultSet.getInt("column1");
                String column2Value = resultSet.getString("column2");

                // Process the retrieved data as needed
                System.out.println("Column1: " + column1Value + ", Column2: " + column2Value);
            }
        }

        // Example: Insert data into a table
        String insertQuery = "INSERT INTO your_table (column1, column2) VALUES (?, ?)";
        try (PreparedStatement preparedStatement = connection.prepareStatement(insertQuery)) {
            // Set values for the prepared statement
            preparedStatement.setInt(1, 123);
            preparedStatement.setString(2, "Example Data");

            // Execute the insert operation
            int rowsAffected = preparedStatement.executeUpdate();

            System.out.println(rowsAffected + " row(s) inserted.");
        }
    }
}
