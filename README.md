package MatisseDemo;

import com.mybank.data.DataSource;
import com.mybank.domain.Account;
import com.mybank.domain.Bank;
import com.mybank.domain.CheckingAccount;
import com.mybank.domain.Customer;
import com.mybank.domain.SavingsAccount;
import com.mybank.reporting.CustomerReport;
import java.io.IOException;
import java.util.logging.Level;
import java.util.logging.Logger;
import javax.swing.JEditorPane;
import javax.swing.JOptionPane;

public class MatisseDemo extends javax.swing.JFrame
{
    public MatisseDemo()
    {
        initComponents();
    }

    private void initComponents()
    {
        jButton1 = new javax.swing.JButton();
        jButton2 = new javax.swing.JButton();
        jButton3 = new javax.swing.JButton();
        jComboBox1 = new javax.swing.JComboBox<>();
        jScrollPane1 = new javax.swing.JScrollPane();
        jEditorPane1 = new javax.swing.JEditorPane("text/html", "");

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);
        setTitle("MyBank Clients");
        setLocationRelativeTo(null);
        setResizable(false);
        
        addWindowListener(new java.awt.event.WindowAdapter()
        {
            public void windowOpened(java.awt.event.WindowEvent evt)
            {
                jComboBox1ActionPerformed(evt);
            }
        });

        jButton1.setText("Show");
        
        jButton1.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jButton1ActionPerformed(evt);
            }
        });

        jButton2.setText("Report");
        
        jButton2.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jButton2ActionPerformed(evt);
            }
        });

        jButton3.setText("About");
        
        jButton3.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jButton3ActionPerformed(evt);
            }
        });

        jComboBox1.setCursor(new java.awt.Cursor(java.awt.Cursor.W_RESIZE_CURSOR));

        jScrollPane1.setViewportView(jEditorPane1);

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        
        layout.setHorizontalGroup
        (
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING).addGroup(layout.createSequentialGroup().addContainerGap().addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING).addComponent(jComboBox1, 0, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE).addComponent(jScrollPane1, javax.swing.GroupLayout.DEFAULT_SIZE, 261, Short.MAX_VALUE)).addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED).addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING, false).addComponent(jButton1, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE).addComponent(jButton2, javax.swing.GroupLayout.DEFAULT_SIZE, 85, Short.MAX_VALUE).addComponent(jButton3, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)).addGap(35, 35, 35))
        );
        
        layout.setVerticalGroup
        (
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING).addGroup(layout.createSequentialGroup().addGap(32, 32, 32).addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE).addComponent(jButton1).addComponent(jComboBox1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)).addGap(18, 18, 18).addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING).addGroup(layout.createSequentialGroup().addComponent(jButton2).addGap(18, 18, 18).addComponent(jButton3)).addComponent(jScrollPane1, javax.swing.GroupLayout.PREFERRED_SIZE, 183, javax.swing.GroupLayout.PREFERRED_SIZE)).addContainerGap(42, Short.MAX_VALUE))
        );

        pack();
    }

    private void jButton3ActionPerformed(java.awt.event.ActionEvent evt)
    {
        JOptionPane.showMessageDialog(this, "Create GUI with help Matisse.");
    }

    private void jComboBox1ActionPerformed(java.awt.event.WindowEvent evt)
    {
        DataSource dataSource = new DataSource("C:\\Users\\Taras\\OneDrive\\Документи\\NetBeansProjects\\GuiLab1\\34-gui-lab1-BilokinTaras\\data\\test.dat");
        
        try
        {
            dataSource.loadData();
        }
        
        catch(IOException ex)
        {
            Logger.getLogger(MatisseDemo.class.getName()).log(Level.SEVERE, null, ex);
        }
            
        for(int i = 0; i < Bank.getNumberOfCustomers(); i++)
        {
            Customer customer = Bank.getCustomer(i);
            jComboBox1.addItem((new StringBuilder()).append(customer.getFirstName()).append(" ").append(customer.getLastName()).toString());
        }
    }

    private void jButton1ActionPerformed(java.awt.event.ActionEvent evt)
    {
        StringBuilder custInfo = new StringBuilder();
                
        Customer customer = Bank.getCustomer(jComboBox1.getSelectedIndex());                                                

        
        custInfo.append(customer.getLastName()).append(" ").append(customer.getFirstName());                                                  
        custInfo.append("<br>Balance: ");
                
        for(int i = 0; i < customer.getNumberOfAccounts(); i++)
        {
            Account account = customer.getAccount(i);
            custInfo.append("$").append(account.getBalance()).append(" ");
        }
 
        jEditorPane1.setText(custInfo.toString());
    }

    private void jButton2ActionPerformed(java.awt.event.ActionEvent evt)
    {        
        StringBuilder custInfo = new StringBuilder();
                
        Customer cust = Bank.getCustomer(jComboBox1.getSelectedIndex());
        custInfo.append(cust.getLastName()).append(" ").append(cust.getFirstName());
        custInfo.append("<br>Account Type: ");
        
        for(int i = 0; i < cust.getNumberOfAccounts(); i++)
        {
            Customer custom = Bank.getCustomer(i);
            Account account = cust.getAccount(i);
                        
            if(account instanceof SavingsAccount)
            { 
                custInfo.append("S ");
            }
        
            else if(account instanceof CheckingAccount)
            {
                custInfo.append("C");
            }
        }
                
        custInfo.append("<br>Balance: ");
                
        for(int j = 0; j < cust.getNumberOfAccounts(); j++)
        {
            Customer custom = Bank.getCustomer(j);
            Account account = cust.getAccount(j);
                    
            custInfo.append("$").append(account.getBalance()).append(" ");
        }
        
        jEditorPane1.setText(custInfo.toString());
    }

    public static void main(String args[])
    {
        java.awt.EventQueue.invokeLater(new Runnable()
        {
            public void run()
            {
                new MatisseDemo().setVisible(true);
            }
        });
    }

    private javax.swing.JButton jButton1;
    private javax.swing.JButton jButton2;
    private javax.swing.JButton jButton3;
    private javax.swing.JComboBox<String> jComboBox1;
    private javax.swing.JScrollPane jScrollPane1;
    private javax.swing.JEditorPane jEditorPane1;
