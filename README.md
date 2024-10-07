
Hallo Semua 😄👋 Pada Tugas Pemograman Berorientasi Objek ini, saya menerapkan program CRUD (Create, Read, Update, Delete) pada java GUI(Graphical User Interfaces). Untuk mengimplementasikan program tersebut saya menggunakan IDE NetBeans dengan menggunakan bahasa pemrograman java dan menggunakan aplikasi pengelola dtabase yaitu postgreSQL.

## Aplikasi
- IDE NetBeans
- PostgreSql
- Java Development Kit 16

## Cara Penggunaan
Buat class java yang berisi program untuk CRUD (create, read, update, delete) kemudian hubungkan Netbeans dengan database di PostgreSql dan juga tambahkan liblary Postgre JDBC driver di projeck yang digunakan untuk program CRUD.
kode program untuk menghubungkan databse dengan kode program java
    
    String driver = "org.postgresql.Driver";
    String koneksi = "jdbc:postgresql://localhost:5432/Your database";
    String user = "postgres";
    String password = "your password";
## Menampilkan data di jTable
Untuk menampilkan data di jTable  sebenarnya kita bisa menggunakan DefaultTbleModel tapi disina saya menggunaka class tanbahan untuk menjadikan agar data bisa ditampilkan di jTable.
    
    import java.awt.event.ActionEvent;
    import java.sql.ResultSet;
    import java.sql.ResultSetMetaData;
    import java.util.Vector;
    import javax.swing.table.DefaultTableModel;
    import javax.swing.table.TableModel;
    public class DbUtils {
    public static TableModel resultSetToTableModel(ResultSet rs) {
        try {
            ResultSetMetaData metaData = rs.getMetaData();
            int numberOfColumns = metaData.getColumnCount();
            Vector columnNames = new Vector();

            // Get the column names
            for (int column = 0; column < numberOfColumns; column++) {
                columnNames.addElement(metaData.getColumnLabel(column + 1));
            }

            Vector rows = new Vector();
            while (rs.next()) {
                Vector newRow = new Vector();

                for (int i = 1; i <= numberOfColumns; i++) {
                    newRow.addElement(rs.getObject(i));
                }

                rows.addElement(newRow);
            }

            return new DefaultTableModel(rows, columnNames);
        } catch (Exception e) {
            e.printStackTrace();

            return null;
        }
    }

    void txtNamaActionPerformed(ActionEvent evt) {
        // TODO add your handling code here:
    }
    }

kemudian program juga ditulis di Main Class untuk menghubungkan dengan DbUtils

       public void tampil() {

        try {
            // TODO code application logi
            Class.forName(driver);
            String sql = "SELECT * FROM tamu";
            conn = DriverManager.getConnection(koneksi, user, password);
            stmt = conn.createStatement();

            while (!conn.isClosed()) {

                ResultSet rs = stmt.executeQuery(sql);
                this.jTable2.setModel(DbUtils.resultSetToTableModel(rs));
                while (rs.next()) {
                    System.out.println(String.valueOf(rs.getObject(1)) + " " + String.valueOf(rs.getObject(2)) + " " + String.valueOf(rs.getObject(3)) + " " + String.valueOf(rs.getObject(4)));
                }
                conn.close();
            }

            stmt.close();

        } catch (ClassNotFoundException ex) {
            Logger.getLogger(PertemuanKeLima.class.getName()).log(Level.SEVERE, null, ex);
        } catch (SQLException ex) {
            Logger.getLogger(PertemuanKeLima.class.getName()).log(Level.SEVERE, null, ex);
        }

    }

dengan menghubungkan dengan posgreSql data akan ditampilkan di jTable

cukup itu yang bisa saya jelaskan semoga mudah difahami dan bisa bermanfaat 😄

