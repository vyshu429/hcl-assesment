import java.sql.*;
import java.util.*;
import java.util.logging.Level;
import java.util.logging.Logger;
class accounter
{
	 private int account_number;
         private int balance;         
	Scanner Ha = new Scanner(System.in);
       
   
	void check_balance()
	{ 
            try{
            Class.forName("com.mysql.cj.jdbc.Driver");  
            Connection con=DriverManager.getConnection( "jdbc:mysql://localhost:3306/banking","root","vyshu123/");   
            Statement stmt=con.createStatement();
            System.out.println("enter account number");
            int a=Ha.nextInt();
            String sql= "select  *from accountants where account_number= ?";
              PreparedStatement stmt1=con.prepareStatement(sql);
              stmt1.setInt(1,a);
            ResultSet rs = stmt1.executeQuery();
                 while(rs.next())   {      
		System.out.println("customer account number is :   "+rs.getString(1));
                System.out.println("balance in account is:   "+rs.getString(5));
                 }
                  con.close();  
}      catch(Exception e)
{    
    System.out.println(e);

}
        }
        void show_transcations()
	{ 
            try{
            Class.forName("com.mysql.cj.jdbc.Driver");  
            Connection con=DriverManager.getConnection( "jdbc:mysql://localhost:3306/banking","root","vyshu123/");   
            Statement stmt=con.createStatement();
            System.out.println("enter account number");
            int a=Ha.nextInt();
            String sql= "select  *from transcations where account_number= ?";
              PreparedStatement stmt1=con.prepareStatement(sql);
              stmt1.setInt(1,a);
            ResultSet rs = stmt1.executeQuery();
            System.out.println("last five transcations are :");
                 for(int i=0;i<5&&rs.last();i++)   {  
                int k=rs.getInt(1);
                System.out.println(k);
                 }
                  con.close();  
}      catch(Exception e)
{    
    System.out.println(e);

}
        }
       
		
	   void transfer()
        {
           
             try{
            Class.forName("com.mysql.cj.jdbc.Driver");  
            Connection con= DriverManager.getConnection( "jdbc:mysql://localhost:3306/banking","root","vyshu123/");  
            System.out.println("enter account number");
            int a=Ha.nextInt();
                 
            String query = "select balance from accountants where account_number= ?";
            PreparedStatement stmt1=con.prepareStatement(query);
            stmt1.setInt(1,a);
            ResultSet rs1 = stmt1.executeQuery();
            int l=0;
            while(rs1.next())   {
        
           
               l= rs1.getInt(1);
            }
                System.out.println("enter money ");
                int m=Ha.nextInt();
                if(l<m)
                {
                    System.out.println("no money");
                }
                else
                {
                    
                l=l-m;
                
             String sql1 = "update accountants set balance=? where account_number=?";
             PreparedStatement stmt2=con.prepareStatement(sql1);
             
             stmt2.setInt(1,l);
             stmt2.setInt(2,a);
int rowAffected = stmt2.executeUpdate();
 PreparedStatement stmt3=con.prepareStatement("insert into transcations values(?,?)");
             stmt3.setInt(1,m);
             stmt3.setInt(2,a);
        
             int i=stmt3.executeUpdate();
            System.out.println(String.format("money transfered ", rowAffected)); 
                }
                  con.close();  
}      catch(Exception e)
{    
    System.out.println(e);

}
            
        }
		
	}



public class newy
{  
	public static void main(String[] args)
	
{    
		Scanner Ha=new Scanner(System.in);
                accounter h=new accounter();
		System.out.print("*******Welcome To INDIAN Bank********** ");
                System.out.println(" \n");
		int ch;
                do{
		
			System.out.println("********Main Menu is*********");
			System.out.println("1.check balance ");
			System.out.println("2.transfer");
                        System.out.println("3.transcations");
                        
		
			System.out.println("  Ur Choice :");
			ch=Ha.nextInt();
			switch(ch)
			{ 
				

				
				case 1:
                                    h.check_balance();
                                    break;
                              
                                 case 2:
                                    h.transfer();
                                    break;
                                 case 3:
                                     h.show_transcations();
                                     break;

			}
                }while(ch!=4);
		}
	
        }
import java.sql.*;
import java.util.*;
import java.util.logging.Level;
import java.util.logging.Logger;
class accounter
{
	 private int account_number;
         private int balance;         
	Scanner Ha = new Scanner(System.in);
       
   
	
        void show_transcations()
	{ 
            try{
            Class.forName("com.mysql.cj.jdbc.Driver");  
            Connection con=DriverManager.getConnection( "jdbc:mysql://localhost:3306/banking","root","vyshhu123/");   
            Statement stmt=con.createStatement();
            System.out.println("enter account number");
            int a=Ha.nextInt();
            String sql= "select  *from transcations where account_number= ?";
              PreparedStatement stmt1=con.prepareStatement(sql);
              stmt1.setInt(1,a);
            ResultSet rs = stmt1.executeQuery();
            
               System.out.println("last five transcations are :");
          
                 for(int i=0;i<5&&rs.next();i++)   {  
                int k=rs.getInt(1);
                System.out.println(k);
                 }
                  con.close();  
}      catch(Exception e)
{    
    System.out.println(e);

}
        }
       
		
	   void transfer()
        {
           
             try{
            Class.forName("com.mysql.cj.jdbc.Driver");  
            Connection con= DriverManager.getConnection( "jdbc:mysql://localhost:3306/banking","root","vyshu123/");  
            System.out.println("enter account number");
            int a=Ha.nextInt();
            String query = "select balance from accountants where account_number= ?";
            PreparedStatement stmt1=con.prepareStatement(query);
            stmt1.setInt(1,a);
            ResultSet rs1 = stmt1.executeQuery();
            int l=0;
            while(rs1.next())   {
               l= rs1.getInt(1);
            }
                System.out.println("enter money ");
                int m=Ha.nextInt();
                if(l<m)
                {
                    System.out.println("no money");
                }
                else
                {
                    
                l=l-m;
                
             String sql1 = "update accountants set balance=? where account_number=?";
             PreparedStatement stmt2=con.prepareStatement(sql1);
             
             stmt2.setInt(1,l);
             stmt2.setInt(2,a);
            int rowAffected = stmt2.executeUpdate();
          
 PreparedStatement stmt3=con.prepareStatement("insert into transcations values(?,?)");
             stmt3.setInt(1,m);
             stmt3.setInt(2,a);
             int i=stmt3.executeUpdate();
            System.out.println(String.format("money transfered ", rowAffected)); 
            String sql= "select  *from accountants where account_number= ?";
              PreparedStatement stmt4=con.prepareStatement(sql);
              stmt4.setInt(1,a);
              ResultSet rs2 = stmt4.executeQuery();
                while(rs2.next())   {      
		System.out.println("customer account number is :   "+rs2.getString(1));
                System.out.println("remaining balance in account is:   "+rs2.getString(5));
                 }
                }
                  con.close();  
}      catch(Exception e)
{    
    System.out.println(e);

}
            
        }
		
	}



public class newy
{  
	public static void main(String[] args)
	
{    
		Scanner Ha=new Scanner(System.in);
                accounter h=new accounter();
		System.out.print("*******Welcome To INDIAN Bank********** ");
                System.out.println(" \n");
		int ch;
                
		
			System.out.println("********Main Menu is*********");
			
			System.out.println("1.transfer");
                        System.out.println("2.transcations");
                        
		
			System.out.println("  Ur Choice :");
			ch=Ha.nextInt();
			switch(ch)
			{ 
			
                                 case 1:
                                    h.transfer();
                                    break;
                                 case 2:
                                     h.show_transcations();
                                     break;

			}
                       
                        
                
		}}
Output:-
	
        } 
 
