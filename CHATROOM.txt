// IMPORTING CLASSES 
import java.awt.BorderLayout;
import java.awt.Frame;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.*;

public class chatclient {
    // DECLARING DIFFERENT COMPONENTS 
    private JDialog aboutDialog;
    private JFrame jf;
    private JTextArea ta;
    private JTextField tf;
    private JButton b1,b2;
    private JComboBox user;
    private JScrollPane pane;
    private JPanel p;
    // INITIALIZING COMPONENTS 
    public chatclient(){
        jf=new JFrame("CHAT ROOM");
        tf=new JTextField(50);
        ta=new JTextArea(10,50);
        b1=new JButton("SEND");
        b2=new JButton("QUIT");
        p=new JPanel();
        user =new JComboBox();
        user.addItem("SATVIK1");
        user.addItem("SATVIK2");
        user.addItem("SATVIK3");
        pane=new JScrollPane(ta,ScrollPaneConstants.VERTICAL_SCROLLBAR_AS_NEEDED,ScrollPaneConstants.HORIZONTAL_SCROLLBAR_NEVER);
    }
    // LAUNCHING GUI FRAME AND SETTING POSITIONS AND SIZES
    public void launch(){
        jf.setLayout(new BorderLayout());
        jf.add(tf,BorderLayout.SOUTH);
        jf.add(pane,BorderLayout.WEST);
        p.setLayout(new GridLayout(3,1));
        p.add(b1);
        p.add(b2);
        p.add(user);
        ta.setEnabled(false);
        jf.add(p,BorderLayout.CENTER);
        // APPLYING ACTION LISTENER TO FORM PERFORM ACTIONS WHEN BUTTON SEND IS PRESSED i.e. COPYING TEXT FROM TEXT FIELD TO TEXT AREA 
        b1.addActionListener(new ActionListener()
        {

            @Override
            public void actionPerformed(ActionEvent ae) {
                String s=tf.getText();
                ta.append(user.getSelectedItem()+":    "+s+"\n");
                tf.setText("");
                ta.setCaretPosition(ta.getDocument().getLength()-1);
            }
        });
        // APPLYING ACTION LISTENER TO FORM PERFORM ACTIONS WHEN BUTTON QUIT IS PRESSED i.e. CLOSING THE GUI INTERFACE 
        b2.addActionListener(new ActionListener(){
            @Override
            public void actionPerformed(ActionEvent ae) {
                System.exit(0);
            }});
        jf.pack();//COMPRESSING DIFFERENT COMPONENTS IN THE FRAME 
        //SET FRAME AS VISIBLE 
        jf.setVisible(true);
        //APPLYING MENU BAR AND ITEMS FILE AND HELP HAVING FUNCTIONS OF QUIT AND ABOUT
        JMenuBar mb=new JMenuBar();
       // ADDING QUIT & FILE
        JMenu file=new JMenu("File");
        JMenuItem quit=new JMenuItem("Quit");
        quit.addActionListener(new ActionListener(){
            // QUIT FUNCTION ON PRESSING FILE->QUIT 
            @Override
            public void actionPerformed(ActionEvent ae) {
                System.exit(0);
            }});
        file.add(quit);
        mb.add(file);     
        // ADDING ABOUT & HELP
        JMenu help=new JMenu("Help");
        JMenuItem about=new JMenuItem("About");
        about.addActionListener(new AboutHandler());
        help.add(about);
        mb.add(help);
        jf.setJMenuBar(mb);//SETTING THE MENU BAR 
   
    }
    //DISPLAYING A DIALOG BOX FOR THE "ABOUT" FUNCTION WHICH DISPLAYS A TEXT ABOUT THE APPLICATION AND CLOSES WHEN OK IS PRESSED  
    private class AboutHandler implements ActionListener{

        @Override
        public void actionPerformed(ActionEvent ae) {
               aboutDialog=new AboutDialog(jf,"About",true);
           
           aboutDialog.setVisible(true);               
        }        
    }
    private class AboutDialog extends JDialog implements ActionListener{
        public AboutDialog(Frame parent,String title,boolean modal){
            super(parent,title,modal);
            add(new JLabel("The ChatClient is a neat tool that allows you to talk other ChatClients via a chat server"),BorderLayout.NORTH);
            JButton b=new JButton("OK");
            add(b,BorderLayout.SOUTH);
            b.addActionListener(this);
            pack();
        }
        @Override
        public void actionPerformed(ActionEvent e){
            setVisible(false);
        }
    }
    // CREATING OBJECT AND FUNCTION CALLING 
public static void main(String[] args){
    chatclient c=new chatclient();
    c.launch();
}
}
