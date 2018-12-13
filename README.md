# Proyecto-3er-parcial
// codigo de index
package autos;
import java.io.*;
import java.sql.*;
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.Timer;

public class Index extends javax.swing.JFrame {
static Connection conn=null;
static Statement st=null;
static ResultSet rs=null;


String frase="LOGIN";
     int n=0;
    public Index() {
        initComponents();
        setSize(480,290);
        setLocation(300,100);

    }
   Timer timer = new Timer (1000, new ActionListener ()
{
    public void actionPerformed(ActionEvent e)
    {
     if (n<2)
     {jLabel4.setText("");
      jLabel4.setText(frase);
      n++;
     }
     else
     {n=0;
       jLabel4.setText("");
      jLabel4.setText("Autos Premier");
     }
    }
});
   private void btningresarActionPerformed(java.awt.event.ActionEvent evt) {                                            
        String user,password,datos;
       user=txtuser.getText();
       password=txtcontra.getText();
      try{
          conn=Main.Enlace(conn);
          rs=Main.login(rs);
          while(rs.next()){
              if(user.equals((String)rs.getString(2))){
                   if(password.equals((String)rs.getString(3))){
                  dispose();

                  JOptionPane.showMessageDialog(null,(String)rs.getString(1)+" Bienvenido a la Intranet");
                new principal().setVisible(true);
                conn.close();
              }else{
                  JOptionPane.showMessageDialog(null,"Usuario o Contraseña Incorrecta Ingrese Denuevo");
                  txtuser.setText("");
                  txtcontra.setText("");
                  txtuser.requestFocus();
              }
              }

          }
      }
      catch(SQLException e){
          JOptionPane.showInternalMessageDialog(null,"Error en conexion"+e.getMessage());
      }
}                                           

    private void b2ActionPerformed(java.awt.event.ActionEvent evt) {                                   
        txtuser.setText("");
        txtcontra.setText("");
        txtuser.requestFocus();
}                                  

    private void b4ActionPerformed(java.awt.event.ActionEvent evt) {                                   
        //new usuarios(this,true).setVisible(true);
        new new_usuario().setVisible(true);
}                                  

    /**
    * @param args the command line arguments
    */
    public static void main(String args[]) {
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new Index().setVisible(true);
            }
        });
    }

    // Variables declaration - do not modify                     
    private javax.swing.JButton b2;
    private javax.swing.JButton b4;
    private javax.swing.JButton btningresar;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel2;
    private javax.swing.JLabel jLabel3;
    private javax.swing.JLabel jLabel4;
    private javax.swing.JLabel jLabel5;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JSeparator jSeparator1;
    private javax.swing.JPasswordField txtcontra;
    private javax.swing.JTextField txtuser;
    // End of variables declaration                   

}

       
