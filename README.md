# Proyecto-3er-parcial
    /* CADA UNO DE ESTOS CODIGOS TIENE SU PROPIO JFRAME CREADO EN NETBEANS */

     // CODIGO DE INDEX.JAVA

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

    //CODIGO  MAIN.JAVA

      package autos;
     import java.io.*;
     import java.sql.*;
    import javax.swing.*;
    public class Main {
    static Connection conn=null;
    static Statement st=null;
    static ResultSet rs=null;

    static String bd="pro_visual";
    static String login="root";
    static String password="";
    static String url="jdbc:mysql://localhost/"+bd;


    public static Connection Enlace(Connection conn) throws SQLException{
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
            conn=DriverManager.getConnection(url, login, password);
        }
        catch(ClassNotFoundException e)
        {
            System.out.print("Clase no Encontrada");
        }
        return conn;
    }
    public static Statement sta (Statement st) throws SQLException{
    conn=Enlace(conn);
    st=conn.createStatement();
    return st;
}

    public static ResultSet Vermarcas(ResultSet rs) throws SQLException{
    st=sta(st);
    String cad;
    cad="select nombre from marca ";
    PreparedStatement prov=conn.prepareStatement(cad);
    rs=prov.executeQuery();
    return rs;
}

     public static ResultSet Vermodelos(ResultSet rs, String mar) throws SQLException{
    st=sta(st);
    String cad;
    cad="SELECT modelo.descripcion from modelo inner join marca on modelo.idmarca=marca.idmarca where marca.nombre='"+mar+"'";
    PreparedStatement prov=conn.prepareStatement(cad);
    rs=prov.executeQuery();
    return rs;
}

    public static ResultSet ObtenerCodMarca(ResultSet rs, String nom)throws SQLException
    {
    st=sta(st);
    String cad;
    cad="select idmarca from marca where nombre='"+nom+"'";
    rs=st.executeQuery(cad);
    return rs;
    }
    public static ResultSet ObtenerCodModelo(ResultSet rs, String nom)throws SQLException
    {
    st=sta(st);
    String cad;
    cad="select idmodelo from modelo where descripcion='"+nom+"'";
    rs=st.executeQuery(cad);
    return rs;
    }
     public static ResultSet ObtenerCodRepuesto(ResultSet rs, String nom)throws SQLException
    {
    st=sta(st);
    String cad;
    cad="select idproducto from productos where nombre='"+nom+"'";
    rs=st.executeQuery(cad);
    return rs;
    }
    public static ResultSet ObtenerCodcliente(ResultSet rs, String nom)throws SQLException
    {
    st=sta(st);
    String cad;
    cad="select idcliente from clientes where apellidos='"+nom+"'";
    rs=st.executeQuery(cad);
    return rs;
    }
    public static ResultSet Enlmarca(ResultSet rs) throws SQLException{
    st=sta(st);
    String cad;
    cad="select * from marca";
    PreparedStatement mar=conn.prepareStatement(cad);
    rs=mar.executeQuery();
    return rs;
     }
    public static ResultSet Enluser(ResultSet rs) throws SQLException{
    st=sta(st);
    String cad;
    cad="select * from usuario";
    PreparedStatement mar=conn.prepareStatement(cad);
    rs=mar.executeQuery();
    return rs;
     }
     public static ResultSet Enlcliente(ResultSet rs) throws SQLException{
    st=sta(st);
    String cad;
    cad="select * from clientes";
    PreparedStatement mar=conn.prepareStatement(cad);
    rs=mar.executeQuery();
    return rs;
     }
     public static ResultSet Enlvautos(ResultSet rs) throws SQLException{
    st=sta(st);
    String cad;
    cad="select * from auto";
    PreparedStatement mar=conn.prepareStatement(cad);
    rs=mar.executeQuery();
    return rs;
       }
     public static ResultSet Enlmodelo(ResultSet rs) throws SQLException{
    st=sta(st);
    String cad;
    cad="select * from ver_modelo";
    PreparedStatement mod=conn.prepareStatement(cad);
    rs=mod.executeQuery();
    return rs;
     }
     public static ResultSet Enlrepuesto(ResultSet rs) throws SQLException{
    st=sta(st);
    String cad;
    cad="select * from productos";
    PreparedStatement mod=conn.prepareStatement(cad);
    rs=mod.executeQuery();
    return rs;
    }

    public static ResultSet login(ResultSet rs) throws SQLException{
        st=sta(st);
        PreparedStatement log=conn.prepareCall("{call login()}");
        rs=log.executeQuery();
        return rs;
    }
    public static ResultSet precio(ResultSet rs,String des) throws SQLException{
        st=sta(st);
        st=sta(st);
    String cad;
    cad="SELECT modelo.precio as total from modelo where modelo.descripcion='"+des+"'";
    rs=st.executeQuery(cad);
    return rs;
    }
      public static ResultSet preciopro(ResultSet rs,String des) throws SQLException{
        st=sta(st);
        st=sta(st);
    String cad;
    cad="SELECT precio from productos where nombre='"+des+"'";
    rs=st.executeQuery(cad);
    return rs;
       }
        public static ResultSet info(ResultSet rs,String nom) throws SQLException{
        st=sta(st);
        st=sta(st);
    String cad;
    cad="SELECT descripcion,precio from productos where nombre='"+nom+"'";
    rs=st.executeQuery(cad);
    return rs;


    }


}

// CODIGO CLIENTE 

    package autos;
     import java.io.*;
      import javax.swing.*;
     import javax.swing.table.*;
     import java.sql.*;
     import autos.Main.*;

    public class clientes extends javax.swing.JFrame {
    static Connection conn=null;
    static Statement st=null;
    static ResultSet rs=null;
    DefaultTableModel dtm=new DefaultTableModel();
    
    /** Creates new form clientes */
    
    public clientes() {
        initComponents();
        String Titulos[]={"DNI","Cliente","Direccion","Telefono"};
        dtm.setColumnIdentifiers(Titulos);
        tbcliente.setModel(dtm);
    }
    private void btngrabarActionPerformed(java.awt.event.ActionEvent evt) {                                          


        int resp;
        resp = JOptionPane.showConfirmDialog(null, "¿Desea Guardar el Registro?", "Pregunta", 0);
        if (resp == 0) {
            try {
                conn = Main.Enlace(conn);
                st = Main.sta(st);
                rs = Main.Enlcliente(rs);
                String nom,ape,dni,dir,tel;
                nom = txtnombre.getText();
                ape = txtapellidos.getText();
                dni = txtdni.getText();
                dir = txtdir.getText();
                tel = txttel.getText();
                PreparedStatement graba = conn.prepareStatement("{call graba_cliente(?,?,?,?,?)}");

                graba.setString(1, dni);
                graba.setString(2, nom);
                graba.setString(3, ape);
                graba.setString(4, dir);
                graba.setString(5, tel);
                graba.executeUpdate();
                JOptionPane.showMessageDialog(null, "Cliente registrado con Exito");
                conn.close();

            } catch (SQLException e) {
                JOptionPane.showMessageDialog(null, "Error en BD" + e.toString());
            }
        }                    // TODO add your handling code here:

    }                                         

    private void btncancelarActionPerformed(java.awt.event.ActionEvent evt) {                                            
        int resp;
        resp=JOptionPane.showConfirmDialog(null,"¿Desea Cancelar el Proceso?","Pregunta", 0);
      /* if(resp==0) {
            limpiar();
            txtcodigo.setEnabled(true);
            activabotones(true,false,false,false);
            cajastexto(false,false,false,false,false,false,false);
        }*/            // TODO add your handling code here:
}                                           

    private void btneditarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        int resp;
        resp=JOptionPane.showConfirmDialog(null,"¿Desea Modificar los Datos?","Pregunta", 0);
        if (resp==0) {
            try {
                conn=Main.Enlace(conn);
                st=Main.sta(st);
                rs=Main.Enlcliente(rs);

                String  nom,ape,dni,dir,tel;

                dni=txtdni.getText();
                nom=txtnombre.getText();
                ape=txtapellidos.getText();
                dir=txtdir.getText();
                tel=txttel.getText();

                PreparedStatement modifica=conn.prepareStatement("{call edita_cliente(?,?,?,?,?)}");
               
                modifica.setString(1, dni);
                modifica.setString(2, nom);
                modifica.setString(3, ape);
                modifica.setString(4, dir);
                modifica.setString(5, tel);

                modifica.executeUpdate();
                JOptionPane.showMessageDialog(null, "Datos modificados con Exito");
                conn.close();

            } catch(SQLException e) {
                JOptionPane.showMessageDialog(null,"Error en BD"+ e.toString());
            }}                      // TODO add your handling code here:
}                                         

    private void btnbuscarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        String b;
        if (btnagregar.isEnabled()) {
            try {
                conn=Main.Enlace(conn);
                rs=Main.Enlcliente(rs);
                b=txtdni.getText();
                boolean encuentra=false;
                String pos;
                while(rs.next()) {
                    if(b.equals(rs.getString(1))) {
                        txtnombre.setText((String)rs.getString(3));
                        txtapellidos.setText((String)rs.getString(4));
                        txtdir.setText((String)rs.getString(5));
                        txttel.setText((String)rs.getString(6));
                        encuentra=true;
                        break;
                    }
                }
                if(encuentra==false) {
                    txtdni.setText("No existe");
                    txtdni.requestFocus();
                }
            } catch(SQLException e) {
                JOptionPane.showMessageDialog(null,"Error BD"+ e.getMessage());
            }
        }        // TODO add your handling code here:
}                                         

    private void btnverActionPerformed(java.awt.event.ActionEvent evt) {                                       
        try {
            int f, i;
            conn=Main.Enlace(conn);
            rs=Main.Enlcliente(rs);
            String datos[]=new String[6];
            f=dtm.getRowCount();
            if(f>0)
                for(i=0;i<f;i++)
                    dtm.removeRow(0);
            while(rs.next()) {
                datos[0]=(String)rs.getString(1);
                datos[1]=(String)rs.getString(3)+' '+(String)rs.getString(4);
                datos[2]=(String)rs.getString(5);
                datos[3]=(String)rs.getString(6);
                dtm.addRow(datos);
            }
        } catch(SQLException e) {
            JOptionPane.showMessageDialog(null,"Error en BD "+e.toString());
        }        // TODO add your handling code here:
}                                      

    /**
    * @param args the command line arguments
    */
    public static void main(String args[]) {
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new clientes().setVisible(true);
            }
        });
    }
    // Variables declaration - do not modify                     
    private javax.swing.JButton btnagregar;
    private javax.swing.JButton btnbuscar;
    private javax.swing.JButton btncancelar;
    private javax.swing.JButton btneditar;
    private javax.swing.JButton btngrabar;
    private javax.swing.JButton btnver;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel10;
    private javax.swing.JLabel jLabel11;
    private javax.swing.JLabel jLabel12;
    private javax.swing.JLabel jLabel14;
    private javax.swing.JLabel jLabel3;
    private javax.swing.JLabel jLabel9;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JPanel jPanel2;
    private javax.swing.JPanel jPanel3;
    private javax.swing.JScrollPane jScrollPane1;
    private javax.swing.JSeparator jSeparator1;
    private javax.swing.JTable tbcliente;
    private javax.swing.JTextField txtapellidos;
    private javax.swing.JTextField txtdir;
    private javax.swing.JTextField txtdni;
    private javax.swing.JTextField txtnombre;
    private javax.swing.JTextField txttel;
    // End of variables declaration                   

    }

    // CODIGO MARCA.JAVA
     package autos;
     import java.io.*;
     import javax.swing.*;
    import javax.swing.table.*;
     import java.sql.*;
     import autos.Main.*;

    public class marca extends javax.swing.JFrame {
    static Connection conn=null;
    static Statement st=null;
    static ResultSet rs=null;
    DefaultTableModel dtm=new DefaultTableModel();
    public marca() {
        initComponents();
        String Titulos[]={"Nª","Marca"};
        dtm.setColumnIdentifiers(Titulos);
        tbmarca.setModel(dtm);
    }
    private void btnbuscarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        String b;
        if (btnagregar.isEnabled()) {
            try {
                conn=Main.Enlace(conn);
                rs=Main.Enlmarca(rs);
                b=txtid.getText();
                boolean encuentra=false;
                String pos;
                while(rs.next()) {
                    if(b.equals(rs.getString(1))) {
                        txtmarca.setText((String)rs.getString(2));
                        txtid.setEnabled(false);
                        encuentra=true;
                        break;
                    }
                }
                if(encuentra==false) {
                    txtid.setText("No existe");
                    txtid.requestFocus();
                }
            } catch(SQLException e) {
                JOptionPane.showMessageDialog(null,"Error BD"+ e.getMessage());
            }
        }        // TODO add your handling code here:
}                                         

    private void btnverActionPerformed(java.awt.event.ActionEvent evt) {                                       
        try {
            int f, i;
            conn=Main.Enlace(conn);
            rs=Main.Enlmarca(rs);
            String datos[]=new String[2];
            f=dtm.getRowCount();
            if(f>0)
                for(i=0;i<f;i++)
                    dtm.removeRow(0);
            while(rs.next()) {
                datos[0]=(String)rs.getString(1);
                datos[1]=(String)rs.getString(2);
                dtm.addRow(datos);
            }
        } catch(SQLException e) {
            JOptionPane.showMessageDialog(null,"Error en BD "+e.toString());
        }        // TODO add your handling code here:
}                                      

    private void btngrabarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        
             
                                        int resp;
                                        resp = JOptionPane.showConfirmDialog(null, "¿Desea Guardar el Registro?", "Pregunta", 0);
                                        if (resp == 0) {
                                            try {
                                                conn = Main.Enlace(conn);
                                                st = Main.sta(st);
                                                rs = Main.Enlmarca(rs);
                                                String m;
                                                m = txtmarca.getText();

                                                PreparedStatement graba = conn.prepareStatement("{call graba_marca(?)}");

                                                graba.setString(1, m);
                                                graba.executeUpdate();

                                                conn.close();                                                
                                                txtid.setEnabled(true);
                                            } catch (SQLException e) {
                                                JOptionPane.showMessageDialog(null, "Error en BD" + e.toString());
                                            }
                                        }                    // TODO add your handling code here:
                                    
        
}                                         

    private void btncancelarActionPerformed(java.awt.event.ActionEvent evt) {                                            
        int resp;
        resp=JOptionPane.showConfirmDialog(null,"¿Desea Cancelar el Proceso?","Pregunta", 0);
      /*  if(resp==0) {
            limpiar();
            txtcodigo.setEnabled(true);
            activabotones(true,false,false,false);
            cajastexto(false,false,false,false,false,false,false);
        }*/            // TODO add your handling code here:
}                                           

    private void btneditarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        int resp;
        resp=JOptionPane.showConfirmDialog(null,"¿Desea Modificar los Datos?","Pregunta", 0);
        if (resp==0) {
            try {
                conn=Main.Enlace(conn);
                st=Main.sta(st);
                rs=Main.Enlmarca(rs);

                String  mar;
                int cod;
                cod=Integer.parseInt(txtid.getText());
                mar=txtmarca.getText();

                PreparedStatement modifica=conn.prepareStatement("{call edit_marca(?,?)}");
                modifica.setInt(1, cod);
                modifica.setString(2, mar);
                
                modifica.executeUpdate();

                conn.close();
                
            } catch(SQLException e) {
                JOptionPane.showMessageDialog(null,"Error en BD"+ e.toString());
            }}                      // TODO add your handling code here:
}                                         

    private void btnagregarActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // TODO add your handling code here:
        txtid.setEnabled(true);
        txtid.setText("");
        txtmarca.setText("");
        txtid.grabFocus();
    }                                          

    /**
    * @param args the command line arguments
    */
    public static void main(String args[]) {
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new marca().setVisible(true);
            }
        });
    }
    // Variables declaration - do not modify                     
    private javax.swing.JButton btnagregar;
    private javax.swing.JButton btnbuscar;
    private javax.swing.JButton btncancelar;
    private javax.swing.JButton btneditar;
    private javax.swing.JButton btngrabar;
    private javax.swing.JButton btnver;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel3;
    private javax.swing.JLabel jLabel6;
    private javax.swing.JLabel jLabel7;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JPanel jPanel2;
    private javax.swing.JPanel jPanel3;
    private javax.swing.JScrollPane jScrollPane1;
    private javax.swing.JScrollPane jScrollPane2;
    private javax.swing.JSeparator jSeparator1;
    private javax.swing.JTable jTable1;
    private javax.swing.JTable tbmarca;
    private javax.swing.JTextField txtid;
    private javax.swing.JTextField txtmarca;
    // End of variables declaration                   

    }
     // CODIGO MODELO
     package autos;
    import java.io.*;
    import javax.swing.*;
    import javax.swing.table.*;
     import java.sql.*;
      import autos.Main.*;

    public class modelo extends javax.swing.JFrame {
    static Connection conn=null;
    static Statement st=null;
    static ResultSet rs=null;
    static ResultSet rs1=null;
    static ResultSet rs2=null;
    boolean yaprogramado=false;
    DefaultTableModel dtm=new DefaultTableModel();
    
    public modelo() {
        initComponents();
        try
            {
                conn=Main.Enlace(conn);
                rs2=Main.Vermarcas(rs2);
                while(rs2.next())
            {
                cbomarca.addItem((String)rs2.getString(1));
            }
        }
     catch(SQLException e)
        {
            JOptionPane.showMessageDialog(null, "Error"+e.getMessage());
        }
        String Titulos[]={"Marca","Modelo","Año","Precio","Colore","Km/s","Tipo"};
        dtm.setColumnIdentifiers(Titulos);
        tbmodelo.setModel(dtm);
    }
     private void btngrabarActionPerformed(java.awt.event.ActionEvent evt) {                                          

        int resp;
        boolean haygrabacion=false;
        resp = JOptionPane.showConfirmDialog(null, "¿Desea Grabar el Registro?", "Pregunta", 0);
        if (resp == 0) {
        try {
                conn = Main.Enlace(conn);
                st = Main.sta(st);
                rs = Main.Enlmodelo(rs);
                String mar,mod,col,tip,a,k,pre;
                int idmar=0;
                mar=(String)cbomarca.getSelectedItem();
                rs1=Main.ObtenerCodMarca(rs1, mar);
                if(rs1.next()) {
                    idmar=Integer.parseInt(rs1.getString(1));
                    haygrabacion=true;
                } else {
                    JOptionPane.showMessageDialog(null,"Seleccione una Marca");
                    haygrabacion=false;
                }
                
                mod=(String)txtmodelo.getText();

               /* if(rbrojo.isSelected()){
                col="Rojo";
                }
                if(rbnegro.isSelected()){
                col="Negro";
                }
                if(rbmarron.isSelected()){
                col="Marron";
                }
                if(rbgris.isSelected()){
                col="Gris";
                }
                if(rbblanco.isSelected()){
                col="Blanco";
                }*/
                col=(String)txtaño.getText();
                tip=(String)cbotipo.getSelectedItem();
                a=(String)txtaño.getText();
                k=(String)txtkm.getText();
                pre=(String)txtprecio.getText();

                if(haygrabacion && !yaprogramado) {
                         PreparedStatement graba=conn.prepareStatement("{call graba_modelo(?,?,?,?,?,?,?)}");
                         graba.setString(1, mod);
                         graba.setString(2, a);
                         graba.setInt(3, idmar);
                         graba.setString(4, pre);
                         graba.setString(5, col);
                         graba.setString(6, k);
                         graba.setString(7, tip);
                         graba.executeUpdate();

                         conn.close();

                         txtid.setEnabled(true);
                                            }
            } catch (SQLException e) {
                JOptionPane.showMessageDialog(null, "Error en BD" + e.toString());
            }
        }                    // TODO add your handling code here:

    }                                         

    private void btncancelarActionPerformed(java.awt.event.ActionEvent evt) {                                            
        int resp;
        resp=JOptionPane.showConfirmDialog(null,"¿Desea Cancelar el Proceso?","Pregunta", 0);
      /*  if(resp==0) {
            limpiar();
            txtcodigo.setEnabled(true);
            activabotones(true,false,false,false);
            cajastexto(false,false,false,false,false,false,false);
        }*/            // TODO add your handling code here:
}                                           

    private void btneditarActionPerformed(java.awt.event.ActionEvent evt) {                                          
    int resp;
        resp=JOptionPane.showConfirmDialog(null,"¿Desea Modificar los Datos?","Pregunta", 0);
        if (resp==0) {
            try {
                conn=Main.Enlace(conn);
                st=Main.sta(st);
                rs=Main.Enlmodelo(rs);

                String mar,des,an,pre,col,vel,tip;
                int codmar=0;

                des=txtmodelo.getText();
                an=txtaño.getText();
                pre=txtprecio.getText();
                col=txtkm.getText();
                vel=txtkm.getText();
                tip=(String)cbotipo.getSelectedItem();;

                mar=(String)cbomarca.getSelectedItem();
                rs1=Main.ObtenerCodMarca(rs1, mar);
                if(rs1.next())
                    codmar=Integer.parseInt(rs1.getString(1));

                
                PreparedStatement modifica=conn.prepareStatement("{call edita_mod(?,?,?,?,?,?,?)}");
                modifica.setInt(1, codmar);
                modifica.setString(2, des);
                modifica.setString(3, an);
                modifica.setString(4, pre);
                modifica.setString(5, col);
                modifica.setString(6, vel);
                modifica.setString(7, tip);
                modifica.executeUpdate();
                JOptionPane.showMessageDialog(null,"Datos modificados correctamente");
                conn.close();
                
            } catch(SQLException e) {
                JOptionPane.showMessageDialog(null,"Error en BD"+ e.toString());
            }}                         // TODO add your handling code here:
}                                         

    private void btnbuscarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        String b;
        if (btnagregar.isEnabled()) {
            try {
                conn=Main.Enlace(conn);
                rs=Main.Enlmodelo(rs);
                b=txtid.getText();
                boolean encuentra=false;
                String pos;
                while(rs.next()) {
                    if(b.equals(rs.getString(1))) {
                        cbomarca.setSelectedItem(rs.getString(1));
                        txtmodelo.setText((String)rs.getString(2));
                        txtaño.setText((String)rs.getString(3));
                        txtprecio.setText((String)rs.getString(4));
                        txtkm.setText((String)rs.getString(6));
                        cbotipo.setSelectedItem(rs.getString(7));
                        txtid.setEnabled(false);

                        encuentra=true;
                        break;
                    }
                }
                if(encuentra==false) {
                    txtid.setText("No existe");
                    txtid.requestFocus();
                }
            } catch(SQLException e) {
                JOptionPane.showMessageDialog(null,"Error BD"+ e.getMessage());
            }
        }        // TODO add your handling code here:
}                                         

    private void btnverActionPerformed(java.awt.event.ActionEvent evt) {                                       
        try {
            int f, i;
            conn=Main.Enlace(conn);
            rs=Main.Enlmodelo(rs);
            String datos[]=new String[7];
            f=dtm.getRowCount();
            if(f>0)
                for(i=0;i<f;i++)
                    dtm.removeRow(0);
            while(rs.next()) {
                datos[0]=(String)rs.getString(1);
                datos[1]=(String)rs.getString(2);
                datos[2]=(String)rs.getString(3);
                datos[3]=(String)rs.getString(4);
                datos[4]=(String)rs.getString(5);
                datos[5]=(String)rs.getString(6);
                datos[6]=(String)rs.getString(7);
                
                dtm.addRow(datos);
            }
        } catch(SQLException e) {
            JOptionPane.showMessageDialog(null,"Error en BD "+e.toString());
        }        // TODO add your handling code here:
}                                      

    /**
    * @param args the command line arguments
    */
    public static void main(String args[]) {
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new modelo().setVisible(true);
            }
        });
    }

    // Variables declaration - do not modify                     
    private javax.swing.JButton btnagregar;
    private javax.swing.JButton btnbuscar;
    private javax.swing.JButton btncancelar;
    private javax.swing.JButton btneditar;
    private javax.swing.JButton btngrabar;
    private javax.swing.JButton btnver;
    private javax.swing.JComboBox cbomarca;
    private javax.swing.JComboBox cbotipo;
    private javax.swing.ButtonGroup grupo;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel10;
    private javax.swing.JLabel jLabel11;
    private javax.swing.JLabel jLabel12;
    private javax.swing.JLabel jLabel13;
    private javax.swing.JLabel jLabel3;
    private javax.swing.JLabel jLabel6;
    private javax.swing.JLabel jLabel7;
    private javax.swing.JLabel jLabel8;
    private javax.swing.JLabel jLabel9;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JPanel jPanel2;
    private javax.swing.JScrollPane jScrollPane1;
    private javax.swing.JSeparator jSeparator1;
    private javax.swing.JRadioButton rbblanco;
    private javax.swing.JRadioButton rbgris;
    private javax.swing.JRadioButton rbmarron;
    private javax.swing.JRadioButton rbnegro;
    private javax.swing.JRadioButton rbrojo;
    private javax.swing.JTable tbmodelo;
    private javax.swing.JTextField txtaño;
    private javax.swing.JTextField txtid;
    private javax.swing.JTextField txtkm;
    private javax.swing.JTextField txtmodelo;
    private javax.swing.JTextField txtprecio;
    // End of variables declaration                   

    }
     //NEW_USUARIO
     Package autos;
     import java.io.*;
           import javax.swing.*;
      //import javax.swing.table.*;
               import java.sql.*;
               import autos.Main.*;

      public class new_usuario extends javax.swing.JFrame {
    static Connection conn=null;
    static Statement st=null;
    static ResultSet rs=null;
  
    public new_usuario() {
        initComponents();
    }
       private void btnagregarActionPerformed(java.awt.event.ActionEvent evt) {                                           
        int resp;
                                        resp = JOptionPane.showConfirmDialog(null, "¿Desea Grabar el Registro?", "Pregunta", 0);
                                        if (resp == 0) {
                                            try {
                                                conn = Main.Enlace(conn);
                                                st = Main.sta(st);
                                                rs = Main.Enluser(rs);
                                                String nom,ape,dn,tel,dir,user,contra;
                                                nom = txtnombre.getText();
                                                ape = txtapellidos.getText();
                                                dn = txtdni.getText();
                                                tel = txttel.getText();
                                                dir = txtdir.getText();
                                                user = txtuser.getText();
                                                contra = txtcontra.getText();
                                                PreparedStatement graba = conn.prepareStatement("{call graba_user(?,?,?,?,?,?,?)}");

                                                graba.setString(1, nom);
                                                graba.setString(2, ape);
                                                graba.setString(3, dn);
                                                graba.setString(4, tel);
                                                graba.setString(5, dir);
                                                graba.setString(6, user);
                                                graba.setString(7, contra);
                                                graba.executeUpdate();
                                                JOptionPane.showMessageDialog(null,"Usuario Registrado correctamente");
                                                
                                                txtnombre.setText("");
                                                txtapellidos.setText("");
                                                txtdni.setText("");
                                                txttel.setText("");
                                                txtdir.setText("");
                                                txtuser.setText("");                                                
                                                txtcontra.setText("");
                                                txtnombre.requestFocus();
                                                dispose();
                                                conn.close();
                                                
                                            } catch (SQLException e) {
                                                JOptionPane.showMessageDialog(null, "Error en BD" + e.toString());
                                            }
                                        }
}                                          

    private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         

        // TODO add your handling code here:
        dispose();
    }                                        

    /**
    * @param args the command line arguments
    */
    public static void main(String args[]) {
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new new_usuario().setVisible(true);
            }
        });
    }

    // Variables declaration - do not modify                     
    private javax.swing.JButton btnagregar;
    private javax.swing.JButton jButton1;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel10;
    private javax.swing.JLabel jLabel11;
    private javax.swing.JLabel jLabel12;
    private javax.swing.JLabel jLabel14;
    private javax.swing.JLabel jLabel2;
    private javax.swing.JLabel jLabel3;
    private javax.swing.JLabel jLabel4;
    private javax.swing.JLabel jLabel9;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JPanel jPanel2;
    private javax.swing.JPanel jPanel3;
    private javax.swing.JSeparator jSeparator1;
    private javax.swing.JTextField txtapellidos;
    private javax.swing.JTextField txtcontra;
    private javax.swing.JTextField txtdir;
    private javax.swing.JTextField txtdni;
    private javax.swing.JTextField txtnombre;
    private javax.swing.JTextField txttel;
    private javax.swing.JTextField txtuser;
    // End of variables declaration                   

     }
     //PRINCIPAL
          package autos;
         import javax.swing.*;
     import java.sql.*;
       import autos.Main.*;
           import javax.swing.table.*;
       import java.util.Date;
              import java.awt.event.KeyEvent;
     public class principal extends javax.swing.JFrame {
    static Connection conn=null;
    static Statement st=null;
    static ResultSet rs=null;
    static ResultSet rs1=null;
    static ResultSet rs2=null;
    static ResultSet rs3=null;
    static ResultSet rs4=null;
    boolean yaprogramado=false;
        DefaultTableModel dtm=new DefaultTableModel();
        DefaultTableModel rep=new DefaultTableModel();
        DefaultListModel l1=new DefaultListModel();
    DefaultListModel l2=new DefaultListModel();
    DefaultListModel l3=new DefaultListModel();
    DefaultListModel l4=new DefaultListModel();
    DefaultListModel l5=new DefaultListModel();
    DefaultListModel l6=new DefaultListModel();
    public principal() {
        initComponents();

        //cliente
        String Titulos[]={"DNI","Cliente","Direccion","Telefono"};
        dtm.setColumnIdentifiers(Titulos);
        tbcliente.setModel(dtm);
        //repuesto
        String repu[]={"Nombre","Descripcion","Precio","Stock"};
        rep.setColumnIdentifiers(repu);
        tbrep.setModel(rep);
        txtruc1.setVisible(false);
        lbruc1.setVisible(false);
        
        //hora
         tiempo re;
    re=new tiempo(lbhora);
    re.start();
     //fecha
    Date d=new Date();
    String fecha=((d.getYear()+1900)+"-"+(d.getMonth()+1)+"-"+d.getDate());
         lbfecha.setText(fecha);
      //fin fecha
        txtruc.setVisible(false);
        lbruc.setVisible(false);
        try //combo marcas
            {
                conn=Main.Enlace(conn);
                rs1=Main.Vermarcas(rs);
                while(rs1.next())
            {
                cbomarca.addItem((String)rs1.getString(1));
            }
        }
     catch(SQLException e)
        {
            JOptionPane.showMessageDialog(null, "Error"+e.getMessage());
        }
          try{ //combo clientes
            conn=Main.Enlace(conn);
            rs=Main.Enlcliente(rs);
            while(rs.next())
             cbocliente.addItem(rs.getString(4));
             rs.close();
        }
        catch(SQLException e){
            JOptionPane.showMessageDialog(null,"Error en Bd"+ e.getMessage());
        }

         try{
            conn=Main.Enlace(conn);
            rs=Main.Enlcliente(rs);
            while(rs.next())
             cboclienterep.addItem(rs.getString(4));
             rs.close();
        }catch(SQLException e){
            JOptionPane.showMessageDialog(null,"Error en Bd"+ e.getMessage());
        }

         try{ //combo productos
            conn=Main.Enlace(conn);
            rs=Main.Enlrepuesto(rs);
            while(rs.next())
             cborep.addItem(rs.getString(2));
        }
        catch(SQLException e){
            JOptionPane.showMessageDialog(null,"Error en Bd"+ e.getMessage());
        }
    
    }
    private void cboxcomprobante1ActionPerformed(java.awt.event.ActionEvent evt) {                                                 
        // TODO add your handling code here:
        String compara;

        compara=(String)cboxcomprobante1.getSelectedItem();
        if(compara.equals("Boleta")){
            txtruc1.setVisible(false);
            lbruc1.setVisible(false);
        }
        if(compara.equals("Factura")){
            txtruc1.setVisible(true);
            lbruc1.setVisible(true);
            txtruc1.requestFocus();

        }
        if(compara.equals("Seleccionar")){
            txtruc1.setVisible(false);
            lbruc1.setVisible(false);
        }
    }                                                

    private void btncancelar3ActionPerformed(java.awt.event.ActionEvent evt) {                                             
        // TODO add your handling code here:
    }                                            

    private void btngrabarrepActionPerformed(java.awt.event.ActionEvent evt) {                                             
        // TODO add your handling code here:
        int resp;
        boolean haygrabacion=false;
        resp=JOptionPane.showConfirmDialog(null,"¿Desea Grabar la venta actual?","Pregunta",0);
        if(resp==0) {
            try {
                conn=Main.Enlace(conn);
                st=Main.sta(st);
                rs=Main.Enlrepuesto(rs);

                String cli,nom,can,tot,com,hor,fec;
                int cod,codcli=0,codnom=0;

                cli=(String)cboclienterep.getSelectedItem();
                rs1=Main.ObtenerCodcliente(rs1, cli);
                if(rs1.next()) {
                    codcli=Integer.parseInt((String)rs1.getString(1));
                    haygrabacion=true;
                } else {
                    JOptionPane.showMessageDialog(null,"Seleccione un Cliente");
                    haygrabacion=false;
                }

                nom=(String)cborep.getSelectedItem();
                rs2=Main.ObtenerCodRepuesto(rs2, nom);
                if(rs2.next()) {
                    codnom=Integer.parseInt((String)rs2.getString(1));
                    haygrabacion=true;
                } else {
                    JOptionPane.showMessageDialog(null,"Seleccione un producto");
                    haygrabacion=false;
                }

                com=(String)cboxcomprobante1.getSelectedItem();

                hor=lbhora.getText();
                fec=lbfecha.getText();
                can=txtcanrep.getText();
                tot=txttotrep.getText();

                if(can.equals("")){
                    JOptionPane.showMessageDialog(null,"Ingrese una cantidad");
                    txtcanrep.requestFocus();
                }else{

                    if(tot.equals("")){
                        JOptionPane.showMessageDialog(null,"Precio no calculado");
                        txttotrep.requestFocus();
                    }else{
                        if(haygrabacion && !yaprogramado) {
                            PreparedStatement graba=conn.prepareStatement("{call graba_ven(?,?,?,?,?,?,?)}");
                            graba.setInt(1, codcli);
                            graba.setInt(2, codnom);
                            graba.setString(3, can);
                            graba.setString(4, fec);
                            graba.setString(5, hor);
                            graba.setString(6, tot);
                            graba.setString(7, com);

                            graba.executeUpdate();
                            JOptionPane.showMessageDialog(null,"Datos de venta registrados con éxito");
                            conn.close();
                            //activabotones(true,false,false,false);
                            //limpiar()
                        }}}
                    } catch(SQLException e) {
                        JOptionPane.showMessageDialog(null,"Error en BD"+e.toString());
                    }
                }
    }                                            

    private void totrepActionPerformed(java.awt.event.ActionEvent evt) {                                       
        // TODO add your handling code here:
        String rep;

        try{
            String res;
            int total,a,b,pre=0;
            rep=(String)cborep.getSelectedItem();
            rs4=Main.preciopro(rs4, rep);
            if(rs4.next())
            pre=Integer.parseInt(rs4.getString(1));

            a=Integer.parseInt(txtcanrep.getText());
            total=a * pre;
            res=String.valueOf(total);
            txttotrep.setText(res);
        }catch(SQLException e) {
            JOptionPane.showMessageDialog(null,"Error en BD"+e.toString());
        }
    }                                      

    private void cborepActionPerformed(java.awt.event.ActionEvent evt) {                                       
        // TODO add your handling code here:
        String rep,inf="";

        try{
            int pre=0;
            rep=(String)cborep.getSelectedItem();
            rs=Main.info(rs, rep);
            if(rs.next())
            inf=(String)rs.getString(1);
            pre=Integer.parseInt(rs.getString(2));
            lbinf.setText("Descripción:"+ inf);
            lbprerep.setText("Precio único:"+ String.valueOf(pre));
        }catch(SQLException e) {
            JOptionPane.showMessageDialog(null,"Error en BD"+e.toString());
        }
    }                                      

    private void editrepActionPerformed(java.awt.event.ActionEvent evt) {                                        
        // TODO add your handling code here:
        int resp;
        resp=JOptionPane.showConfirmDialog(null,"¿Desea Modificar los Datos?","Pregunta", 0);
        if (resp==0) {
            try {
                conn=Main.Enlace(conn);
                st=Main.sta(st);
                rs=Main.Enlrepuesto(rs);

                String  nom,des,pre,st;

                nom=txtnrep.getText();
                des=txtdes.getText();
                pre=txtpre.getText();
                st=txtst.getText();

                PreparedStatement modifica=conn.prepareStatement("{call edita_rep(?,?,?,?)}");

                modifica.setString(1,nom);
                modifica.setString(2, des);
                modifica.setString(3, pre);
                modifica.setString(4, st);

                modifica.executeUpdate();
                JOptionPane.showMessageDialog(null, "Datos modificados con Exito");
                conn.close();

            } catch(SQLException e) {
                JOptionPane.showMessageDialog(null,"Error en BD"+ e.toString());
            }}
    }                                       

    private void btncancelar2ActionPerformed(java.awt.event.ActionEvent evt) {                                             
        // TODO add your handling code here:
    }                                            

    private void grabrepActionPerformed(java.awt.event.ActionEvent evt) {                                        
        // TODO add your handling code here:
        int resp;
        resp = JOptionPane.showConfirmDialog(null, "¿Desea Grabar el Registro?", "Pregunta", 0);
        if (resp == 0) {
            try {
                conn = Main.Enlace(conn);
                st = Main.sta(st);
                rs = Main.Enlrepuesto(rs);
                String nom,des,pre,st;
                nom = txtnrep.getText();
                des = txtdes.getText();
                pre = txtpre.getText();
                st = txtst.getText();

                PreparedStatement graba = conn.prepareStatement("{call graba_repuesto(?,?,?,?)}");

                graba.setString(1, nom);
                graba.setString(2, des);
                graba.setString(3, pre);
                graba.setString(4, st);

                graba.executeUpdate();
                JOptionPane.showMessageDialog(null, "Repuesto registrado con Exito");
                conn.close();

            } catch (SQLException e) {
                JOptionPane.showMessageDialog(null, "Error en BD" + e.toString());
            }
        }
    }                                       

    private void verrepActionPerformed(java.awt.event.ActionEvent evt) {                                       
        // TODO add your handling code here:
        try {
            int f, i;
            conn=Main.Enlace(conn);
            rs=Main.Enlrepuesto(rs);
            String repuesto[]=new String[4];
            f=rep.getRowCount();
            if(f>0)
            for(i=0;i<f;i++)
            rep.removeRow(0);
            while(rs.next()) {
                repuesto[0]=(String)rs.getString(2);
                repuesto[1]=(String)rs.getString(3);
                repuesto[2]=(String)rs.getString(4);
                repuesto[3]=(String)rs.getString(5);
                rep.addRow(repuesto);
            }
        } catch(SQLException e) {
            JOptionPane.showMessageDialog(null,"Error en BD "+e.toString());
        }
    }                                      

    private void busrepActionPerformed(java.awt.event.ActionEvent evt) {                                       
        // TODO add your handling code here:
        String b;
        if (btnagregar.isEnabled()) {
            try {
                conn=Main.Enlace(conn);
                rs=Main.Enlrepuesto(rs);
                b=txtnrep.getText();
                boolean encuentra=false;
                String pos;
                while(rs.next()) {
                    if(b.equals(rs.getString(2))) {

                        txtdes.setText((String)rs.getString(3));
                        txtpre.setText((String)rs.getString(4));
                        txtst.setText((String)rs.getString(5));
                        encuentra=true;
                        break;
                    }
                }
                if(encuentra==false) {
                    txtnrep.setText("No existe");
                    txtnrep.requestFocus();
                }
            } catch(SQLException e) {
                JOptionPane.showMessageDialog(null,"Error BD"+ e.getMessage());
            }
        }
    }                                      

    private void btneditarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        int resp;
        resp=JOptionPane.showConfirmDialog(null,"¿Desea Modificar los Datos?","Pregunta", 0);
        if (resp==0) {
            try {
                conn=Main.Enlace(conn);
                st=Main.sta(st);
                rs=Main.Enlcliente(rs);

                String  nom,ape,dni,dir,tel;

                dni=txtdni.getText();
                nom=txtnombre.getText();
                ape=txtapellidos.getText();
                dir=txtdir.getText();
                tel=txttel.getText();

                PreparedStatement modifica=conn.prepareStatement("{call edita_cliente(?,?,?,?,?)}");

                modifica.setString(1, dni);
                modifica.setString(2, nom);
                modifica.setString(3, ape);
                modifica.setString(4, dir);
                modifica.setString(5, tel);

                modifica.executeUpdate();
                JOptionPane.showMessageDialog(null, "Datos modificados con Exito");
                conn.close();

            } catch(SQLException e) {
                JOptionPane.showMessageDialog(null,"Error en BD"+ e.toString());
            }}                      // TODO add your handling code here:
    }                                         

    private void btncancelar1ActionPerformed(java.awt.event.ActionEvent evt) {                                             
        int resp;
        resp=JOptionPane.showConfirmDialog(null,"¿Desea Cancelar el Proceso?","Pregunta", 0);
        /* if(resp==0) {
            limpiar();
            txtcodigo.setEnabled(true);
            activabotones(true,false,false,false);
            cajastexto(false,false,false,false,false,false,false);
        }*/            // TODO add your handling code here:
    }                                            

    private void btngrabar1ActionPerformed(java.awt.event.ActionEvent evt) {                                           

        int resp;
        resp = JOptionPane.showConfirmDialog(null, "¿Desea Grabar el Registro?", "Pregunta", 0);
        if (resp == 0) {
            try {
                conn = Main.Enlace(conn);
                st = Main.sta(st);
                rs = Main.Enlcliente(rs);
                String nom,ape,dni,dir,tel;
                nom = txtnombre.getText();
                ape = txtapellidos.getText();
                dni = txtdni.getText();
                dir = txtdir.getText();
                tel = txttel.getText();
                PreparedStatement graba = conn.prepareStatement("{call graba_cliente(?,?,?,?,?)}");

                graba.setString(1, dni);
                graba.setString(2, nom);
                graba.setString(3, ape);
                graba.setString(4, dir);
                graba.setString(5, tel);
                graba.executeUpdate();
                JOptionPane.showMessageDialog(null, "Cliente registrado con Exito");
                conn.close();

            } catch (SQLException e) {
                JOptionPane.showMessageDialog(null, "Error en BD" + e.toString());
            }
        }                    // TODO add your handling code here:
    }                                          

    private void btnverActionPerformed(java.awt.event.ActionEvent evt) {                                       
        try {
            int f, i;
            conn=Main.Enlace(conn);
            rs=Main.Enlcliente(rs);
            String datos[]=new String[5];
            f=dtm.getRowCount();
            if(f>0)
            for(i=0;i<f;i++)
            dtm.removeRow(0);
            while(rs.next()) {
                datos[0]=(String)rs.getString(2);
                datos[1]=(String)rs.getString(3)+' '+(String)rs.getString(4);
                datos[2]=(String)rs.getString(5);
                datos[3]=(String)rs.getString(6);
                dtm.addRow(datos);
            }
        } catch(SQLException e) {
            JOptionPane.showMessageDialog(null,"Error en BD "+e.toString());
        }        // TODO add your handling code here:
    }                                      

    private void btnbuscarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        String b;
        if (btnagregar.isEnabled()) {
            try {
                conn=Main.Enlace(conn);
                rs=Main.Enlcliente(rs);
                b=txtdni.getText();
                boolean encuentra=false;
                String pos;
                while(rs.next()) {
                    if(b.equals(rs.getString(2))) {
                        txtnombre.setText((String)rs.getString(3));
                        txtapellidos.setText((String)rs.getString(4));
                        txtdir.setText((String)rs.getString(5));
                        txttel.setText((String)rs.getString(6));
                        encuentra=true;
                        break;
                    }
                }
                if(encuentra==false) {
                    txtdni.setText("No existe");
                    txtdni.requestFocus();
                }
            } catch(SQLException e) {
                JOptionPane.showMessageDialog(null,"Error BD"+ e.getMessage());
            }
        }        // TODO add your handling code here:
    }                                         

    private void cboxcomprobanteActionPerformed(java.awt.event.ActionEvent evt) {                                                
        String compara;

        compara=(String)cboxcomprobante.getSelectedItem();
        if(compara.equals("Boleta")){
            txtruc.setVisible(false);
            lbruc.setVisible(false);
        }
        if(compara.equals("Factura")){
            txtruc.setVisible(true);
            lbruc.setVisible(true);
            txtruc.requestFocus();

        }
        if(compara.equals("Seleccionar")){
            txtruc.setVisible(false);
            lbruc.setVisible(false);
        }

    }                                               

    private void btncancelarActionPerformed(java.awt.event.ActionEvent evt) {                                            
        /* l1.removeAllElements();
        l2.removeAllElements();
        l3.removeAllElements();
        l4.removeAllElements();
        txtcantidad.setText("");
        txtprobuscar.setText("");
        l5.removeAllElements();
        l6.removeAllElements();
        txttotalpagar.setText("");
        botonesagregar(false,false);
        botonesagregar(false,false);
        cajastexto(false,false,false,false,false,false,false);
        activabotones(true,false,false,false);
        txtcliente.setText("");
        cbocliente.setSelectedIndex(0);
        txtruc.setText("");
        rbtnnuevo.setSelected(false);
        rbtnregistrado.setSelected(false);*/
    }                                           

    private void btngrabarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        int resp;
        boolean haygrabacion=false;
        resp=JOptionPane.showConfirmDialog(null,"¿Desea Grabar la venta actual?","Pregunta",0);
        if(resp==0) {
            try {
                conn=Main.Enlace(conn);
                st=Main.sta(st);
                rs=Main.Enlvautos(rs);

                String mar,mod,compr,ruc,tip,col,cant,total,cliente_n,fecha,hora,cregistrado;
                int cod,codmar=0,codmod=0,codcli=0;

                mar=(String)cbomarca.getSelectedItem();
                rs1=Main.ObtenerCodMarca(rs1, mar);
                if(rs1.next()) {
                    codmar=Integer.parseInt((String)rs1.getString(1));
                    haygrabacion=true;
                } else {
                    JOptionPane.showMessageDialog(null,"Seleccione una marca");
                    haygrabacion=false;
                }

                mod=(String)cbomodelo.getSelectedItem();
                rs2=Main.ObtenerCodModelo(rs2, mod);
                if(rs2.next()) {
                    codmod=Integer.parseInt((String)rs2.getString(1));
                    haygrabacion=true;
                } else {
                    JOptionPane.showMessageDialog(null,"Seleccione un Modelo");
                    haygrabacion=false;
                }

                mod=(String)cbocliente.getSelectedItem();
                rs3=Main.ObtenerCodcliente(rs3, mod);
                if(rs3.next()) {
                    codcli=Integer.parseInt((String)rs3.getString(1));
                    haygrabacion=true;
                } else {
                    JOptionPane.showMessageDialog(null,"Seleccione un Cliente");
                    haygrabacion=false;
                }

                compr=(String)cboxcomprobante.getSelectedItem();
                ruc=txtruc.getText();
                tip=(String)cbotipo.getSelectedItem();
                col=(String)cbocolor.getSelectedItem();
                cant=txtcan.getText();
                hora=lbhora.getText();
                fecha=lbfecha.getText();
                total=lbtotal.getText();
                //cregistrado=(String)cbocliente.getSelectedItem();

                if(((String)cboxcomprobante.getSelectedItem()).equals("Seleccionar")){
                    JOptionPane.showMessageDialog(null,"Seleccione un Comprobante");
                    cboxcomprobante.requestFocus();
                }else{
                    if(((String)cbomarca.getSelectedItem()).equals("...Elegir...")){
                        JOptionPane.showMessageDialog(null,"Seleccione una marca");
                        cbomarca.requestFocus();
                    }else{
                        if(((String)cbotipo.getSelectedItem()).equals("...Elegir...")){
                            JOptionPane.showMessageDialog(null,"Seleccione un tipo de Auto");
                            cbotipo.requestFocus();
                        }else{

                            if(((String)cbocolor.getSelectedItem()).equals("...Elegir...")){
                                JOptionPane.showMessageDialog(null,"Seleccione un color");
                                cbocolor.requestFocus();
                            }else{
                                if(((String)cbomodelo.getSelectedItem()).equals("...Elegir...")){
                                    JOptionPane.showMessageDialog(null,"Seleccione un tipo de Modelo");
                                    cbomodelo.requestFocus();
                                }else{
                                    if(ruc.equals("")){
                                        JOptionPane.showMessageDialog(null,"Ingrese su numero de RUC");
                                        txtruc.requestFocus();
                                    }else{

                                        if(cant.equals("")){
                                            JOptionPane.showMessageDialog(null,"Ingrese una cantidad determinada");
                                            txtruc.requestFocus();
                                        }else{
                                            if(haygrabacion && !yaprogramado) {
                                                PreparedStatement graba=conn.prepareStatement("{call graba_v_auto(?,?,?,?,?,?,?,?,?,?,?)}");
                                                graba.setInt(1, codcli);
                                                graba.setInt(2, codmar);
                                                graba.setInt(3, codmod);
                                                graba.setString(4, compr);
                                                graba.setString(5, ruc);
                                                graba.setString(6, tip);
                                                graba.setString(7, col);
                                                graba.setString(8, cant);
                                                graba.setString(9, total);
                                                graba.setString(10, fecha);
                                                graba.setString(11, hora);
                                                graba.executeUpdate();
                                                JOptionPane.showMessageDialog(null,"Datos de venta registrados con éxito");
                                                conn.close();
                                                //activabotones(true,false,false,false);
                                                //limpiar()
                                            }}}}}}}}
                                        } catch(SQLException e) {
                                            JOptionPane.showMessageDialog(null,"Error en BD"+e.toString());
                                        }
                                    }
    }                                         

    private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
        String mod;

        try{
            String res;
            int total,a,b,pre=0;
            mod=(String)cbomodelo.getSelectedItem();
            rs4=Main.precio(rs4, mod);
            if(rs4.next())
            pre=Integer.parseInt(rs4.getString(1));

            a=Integer.parseInt(txtcan.getText());
            total=a * pre;
            res=String.valueOf(total);
            lbtotal.setText(res);
        }catch(SQLException e) {
            JOptionPane.showMessageDialog(null,"Error en BD"+e.toString());
        }
    }                                        

    private void cbotipoActionPerformed(java.awt.event.ActionEvent evt) {                                        
        // TODO add your handling code here:
    }                                       

    private void cbomodeloActionPerformed(java.awt.event.ActionEvent evt) {                                          
        // TODO add your handling code here:
        String mod;

        try{
            int pre=0;
            mod=(String)cbomodelo.getSelectedItem();
            rs4=Main.precio(rs4, mod);
            if(rs4.next())
            pre=Integer.parseInt(rs4.getString(1));
            lbprecio.setText("El precio de dicho modelo es de:"+ String.valueOf(pre));
        }catch(SQLException e) {
            JOptionPane.showMessageDialog(null,"Error en BD"+e.toString());
        }
    }                                         

    private void btnmodelo1ActionPerformed(java.awt.event.ActionEvent evt) {                                           

        // TODO add your handling code here:
        String mar;
        mar=(String)cbomarca.getSelectedItem();
        try {
            conn=Main.Enlace(conn);
            rs=Main.Vermodelos(rs, mar);

            while(rs.next()) {
                cbomodelo.addItem((String)rs.getString(1));

                this.setSize(580,400);
            }
        } catch(SQLException e) {
            JOptionPane.showMessageDialog(null, "Error"+e.getMessage());
        }
    }                                          

    private void cbocolorActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
    }                                        

    private void cbomarcaActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
    }                                        

    private void jMenuItem7ActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // TODO add your handling code here:
        rep_cliente.visualiza();
    }                                          

    private void jMenuItem3ActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // TODO add your handling code here:
        cliente.setVisible(true);
    }                                          

    private void jMenuItem6ActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // TODO add your handling code here:
        repuestos.setVisible(true);
    }                                          

    private void jMenuItem2ActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // TODO add your handling code here:
        vrep.setVisible(true);
    }                                          

    private void jMenuItem1ActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // TODO add your handling code here:
        auto.setVisible(true);
    }                                          



    // venta de repuesto

    /**
    * @param args the command line arguments
    */
    public static void main(String args[]) {
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new principal().setVisible(true);
            }
        });
    }

    // Variables declaration - do not modify                     
    private javax.swing.JInternalFrame auto;
    private javax.swing.JButton btnagregar;
    private javax.swing.JButton btnagregar1;
    private javax.swing.JButton btnbuscar;
    private javax.swing.JButton btncancelar;
    private javax.swing.JButton btncancelar1;
    private javax.swing.JButton btncancelar2;
    private javax.swing.JButton btncancelar3;
    private javax.swing.JButton btneditar;
    private javax.swing.JButton btngrabar;
    private javax.swing.JButton btngrabar1;
    private javax.swing.JButton btngrabarrep;
    private javax.swing.JButton btnmodelo1;
    private javax.swing.JButton btnver;
    private javax.swing.JButton busrep;
    private javax.swing.ButtonGroup buttonGroup1;
    private javax.swing.JComboBox cbocliente;
    private javax.swing.JComboBox cboclienterep;
    private javax.swing.JComboBox cbocolor;
    private javax.swing.JComboBox cbomarca;
    private javax.swing.JComboBox cbomodelo;
    private javax.swing.JComboBox cborep;
    private javax.swing.JComboBox cbotipo;
    private javax.swing.JComboBox cboxcomprobante;
    private javax.swing.JComboBox cboxcomprobante1;
    private javax.swing.JInternalFrame cliente;
    private javax.swing.JButton editrep;
    private javax.swing.JButton grabrep;
    private javax.swing.JButton jButton1;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel10;
    private javax.swing.JLabel jLabel11;
    private javax.swing.JLabel jLabel12;
    private javax.swing.JLabel jLabel13;
    private javax.swing.JLabel jLabel14;
    private javax.swing.JLabel jLabel15;
    private javax.swing.JLabel jLabel16;
    private javax.swing.JLabel jLabel17;
    private javax.swing.JLabel jLabel19;
    private javax.swing.JLabel jLabel20;
    private javax.swing.JLabel jLabel21;
    private javax.swing.JLabel jLabel22;
    private javax.swing.JLabel jLabel23;
    private javax.swing.JLabel jLabel3;
    private javax.swing.JLabel jLabel5;
    private javax.swing.JLabel jLabel8;
    private javax.swing.JLabel jLabel9;
    private javax.swing.JMenu jMenu1;
    private javax.swing.JMenu jMenu2;
    private javax.swing.JMenu jMenu3;
    private javax.swing.JMenuBar jMenuBar1;
    private javax.swing.JMenuItem jMenuItem1;
    private javax.swing.JMenuItem jMenuItem2;
    private javax.swing.JMenuItem jMenuItem3;
    private javax.swing.JMenuItem jMenuItem4;
    private javax.swing.JMenuItem jMenuItem5;
    private javax.swing.JMenuItem jMenuItem6;
    private javax.swing.JMenuItem jMenuItem7;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JPanel jPanel10;
    private javax.swing.JPanel jPanel11;
    private javax.swing.JPanel jPanel12;
    private javax.swing.JPanel jPanel13;
    private javax.swing.JPanel jPanel14;
    private javax.swing.JPanel jPanel2;
    private javax.swing.JPanel jPanel3;
    private javax.swing.JPanel jPanel4;
    private javax.swing.JPanel jPanel5;
    private javax.swing.JPanel jPanel6;
    private javax.swing.JPanel jPanel7;
    private javax.swing.JPanel jPanel8;
    private javax.swing.JPanel jPanel9;
    private javax.swing.JScrollPane jScrollPane1;
    private javax.swing.JScrollPane jScrollPane2;
    private javax.swing.JScrollPane jScrollPane3;
    private javax.swing.JSeparator jSeparator1;
    private javax.swing.JLabel lbfecha;
    private javax.swing.JLabel lbhora;
    private javax.swing.JLabel lbinf;
    private javax.swing.JLabel lbprecio;
    private javax.swing.JLabel lbprerep;
    private javax.swing.JLabel lbruc;
    private javax.swing.JLabel lbruc1;
    private javax.swing.JLabel lbtotal;
    private javax.swing.JInternalFrame repuestos;
    private javax.swing.JTable tbcliente;
    private javax.swing.JTable tbrep;
    private javax.swing.JButton totrep;
    private javax.swing.JTextField txtapellidos;
    private javax.swing.JTextField txtcan;
    private javax.swing.JTextField txtcanrep;
    private javax.swing.JTextArea txtdes;
    private javax.swing.JTextField txtdir;
    private javax.swing.JTextField txtdni;
    private javax.swing.JTextField txtnombre;
    private javax.swing.JTextField txtnrep;
    private javax.swing.JTextField txtpre;
    private javax.swing.JTextField txtruc;
    private javax.swing.JTextField txtruc1;
    private javax.swing.JTextField txtst;
    private javax.swing.JTextField txttel;
    private javax.swing.JTextField txttotrep;
    private javax.swing.JButton verrep;
    private javax.swing.JInternalFrame vrep;
    // End of variables declaration                   

    }
    //REP_CLIENTE
    package autos;
     import java.sql.*;
       import javax.swing.JOptionPane;
             import java.util.HashMap;
     import java.util.Map;
      import net.sf.jasperreports.engine.JasperFillManager;
         import net.sf.jasperreports.engine.JasperPrint;
          import net.sf.jasperreports.view.JasperViewer;
      import autos.Main.*;
     /**
        *
              * @author Carlos
       */
              public class rep_cliente {
          static Connection conn=null;
         public static void visualiza()
        {
    try
            {
        conn=Main.Enlace(conn);
        conn.setAutoCommit(false);
     }
    catch(SQLException e)
            {
        JOptionPane.showMessageDialog(null, e.getMessage());
    }
    try
    {
        Map parameters=new HashMap();
        parameters.put("","");
        JasperPrint print=JasperFillManager.fillReport(System.getProperty("user.dir")+
        "/reportes/cliente.jasper",parameters,conn);
     JasperViewer.viewReport(print,false);
         }
                catch(Exception e)
        {
            e.printStackTrace();
       }
       }
       }
       //CODIGO TIEMPO
       package autos;
      import java.awt.*;
       import java.util.*;
           import javax.swing.*;
               import javax.swing.JLabel;

      public class tiempo extends Thread{
     private int horas=0;
            private int minutos=0;
          private int segundos=0;
    private JLabel txtaux;
    public static void main(String[] args) {
    }

    tiempo(JLabel lbhora) {
        Calendar c=Calendar.getInstance();
        horas=c.getTime().getHours();
         minutos=c.getTime().getMinutes();
          segundos=c.getTime().getSeconds();
          txtaux=lbhora;
          this.mostrarHora(txtaux);
    }
    public void run()
    {
     while(true)
     {//paramos 1 segundo
      try
        {Thread.sleep(1000);
        }
      catch(InterruptedException ex)
      {ex.printStackTrace();
      }
      //incrementamos 1 segundo
      segundos++;
      if(segundos==60){
         segundos=0;
         minutos++;
       if(minutos==60){
          minutos=0;
          horas++;
       if(horas==24){
          horas=0;
       }}}
      this.mostrarHora(txtaux);
     }}
    public void mostrarHora(JLabel Txtime)
     {//formatear hora}
    StringBuffer tmp=new StringBuffer(8);
    if(horas<10)
    {tmp.append(0);
    }
    tmp.append(horas);
    tmp.append(":");
    if(minutos<10)
    {tmp.append(0);
    }
    tmp.append(minutos);
    tmp.append(":");
    if(segundos<10)
      {tmp.append(0);
      }
    tmp.append(segundos);
    Txtime.setText(tmp.toString());
    }
     }




   








       
