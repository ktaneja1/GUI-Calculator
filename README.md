# GUI-Calculator
A small project in which I create a GUI interest calculator using java. 

package calculator;

import java.awt.*;

import java.awt.event.*;
import java.awt.event.ActionListener;
import java.text.NumberFormat;

import javax.swing.*;
import javax.swing.border.TitledBorder;

public class InterestGUI extends JFrame {

	//This is where the text fields have been created
	private JTextField principal = new JTextField();
	private JTextField rate = new JTextField();
	private JTextField years = new JTextField();
	private JTextField simpleInterestAnswer = new JTextField();
	private JTextField compoundInterestAnswer= new JTextField();

	// Bellow are the names of the buttons
	private JButton simpleInterest = new JButton("Compute Simple Interest");
	private JButton compoundInterest = new JButton("Compute Compoud Interest");

	JTextArea area = new JTextArea(20, 20);

	public InterestGUI() {
		// panel panel to hold labels and text fields
		JPanel panel1 = new JPanel(new GridLayout(10,6));
		panel1.add(new JLabel("Enter Principal"));
		panel1.add(principal);
		panel1.add(new JLabel("Enter Rate"));
		panel1.add(rate);
		panel1.add(new JLabel("Enter Years"));
		panel1.add(years);
		panel1.add(new JLabel("Answer:"));
		panel1.add(simpleInterestAnswer);
		panel1.add(compoundInterestAnswer);
		simpleInterestAnswer.setEditable(false);
		compoundInterestAnswer.setEditable(false);

		//Here a new panel is made and the interest rates are added and then the panels are added to the frame
		JPanel panel2 = new JPanel();
		panel2.add(simpleInterest);
		panel2.add(compoundInterest);


		add(panel1, BorderLayout.CENTER);
		add(panel2, BorderLayout.SOUTH);


		/*The action listener checks what button has been clicked by the user. If the user selects 'calculate simple 
		 * interest then the code below will execute. It gets the principal, rate, and years and gets put into the 
		 * formula. The answer is set into simpleInterestAnswer.
		 */
		simpleInterest.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				double principalTxt = Double.parseDouble(principal.getText());
				double rateTxt = Double.parseDouble(rate.getText());
				double yearsTxt = Double.parseDouble(years.getText());

				String simpInterest ="Simple Interest Rate: "+
						NumberFormat.getCurrencyInstance().format(principalTxt+(principalTxt*(rateTxt/100) *yearsTxt));

				simpleInterestAnswer.setText((simpInterest));
			}
		});

		/*The action listener checks what button has been clicked by the user. If the user selects 'calculate compound 
		 *interest then the code below will execute. It gets the principal, rate, and years and gets put into the 
		 *formula. The answer is set into compoundInterestAnswer.
		 */
		compoundInterest.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {

				double principalTxt = Double.parseDouble(principal.getText());
				double rateTxt = Double.parseDouble(rate.getText());
				double yearsTxt = Double.parseDouble(years.getText());
				//	double value= (principalTxt* Math.pow(1+rateTxt/100, yearsTxt));
				//String compInterest= "Compound Interest Rate: "+NumberFormat.getCurrencyInstance().format(value);
				String compInterest=""+NumberFormat.getCurrencyInstance().format
						( principalTxt* (Math.pow(1+rateTxt/100, yearsTxt)));
				compoundInterestAnswer.setText((compInterest));

			}
		});
	}

	/*In the main method, the calculator is made. The size and title are set. Pack is used to help keep 
	 * the format if the window is resized. 
	 * the window. 
	 * 
	 */
	public static void main(String[] args) {
		InterestGUI calculator = new InterestGUI();
		calculator.setSize(1000, 1000);
		calculator.setTitle("Interest Calculator ");
		calculator.pack();
		calculator.setResizable(true);
		calculator.setVisible(true);
		calculator.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); //Closes the window at users will.
	}
}
