package projetocep;

import java.awt.Cursor;
import java.awt.EventQueue;
import java.awt.SystemColor;
import java.awt.Toolkit;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.net.URL;

import javax.swing.DefaultComboBoxModel;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JTextField;
import javax.swing.border.EmptyBorder;

import org.dom4j.Document;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

public class CEP extends JFrame {

	private static final long serialVersionUID = 1L;
	private JPanel contentPane;
	private JTextField txtCep;
	private JTextField txtEndereco;
	private JTextField txtBairro;
	private JTextField txtCidade;
	private JComboBox<String> cbpUf;

	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					CEP frame = new CEP();
					frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	public CEP() {
		setTitle("Buscar CEP");
		setResizable(false);
		setIconImage(Toolkit.getDefaultToolkit().getImage(CEP.class.getResource("/img/home.png")));
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 450, 300);
		contentPane = new JPanel();
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		contentPane.setLayout(null);

		JLabel lblNewLabel = new JLabel("CEP");
		lblNewLabel.setBounds(38, 58, 45, 13);
		contentPane.add(lblNewLabel);

		txtCep = new JTextField();
		txtCep.setBounds(107, 55, 115, 19);
		contentPane.add(txtCep);
		txtCep.setColumns(10);

		JLabel lblNewLabel_1 = new JLabel("Endereço");
		lblNewLabel_1.setBounds(38, 103, 70, 13);
		contentPane.add(lblNewLabel_1);

		JLabel lblNewLabel_2 = new JLabel("Bairro");
		lblNewLabel_2.setBounds(38, 138, 45, 13);
		contentPane.add(lblNewLabel_2);

		JLabel lblNewLabel_3 = new JLabel("Cidade");
		lblNewLabel_3.setBounds(38, 178, 45, 13);
		contentPane.add(lblNewLabel_3);

		txtEndereco = new JTextField();
		txtEndereco.setBounds(107, 100, 234, 19);
		contentPane.add(txtEndereco);
		txtEndereco.setColumns(10);

		txtBairro = new JTextField();
		txtBairro.setBounds(107, 135, 234, 19);
		contentPane.add(txtBairro);
		txtBairro.setColumns(10);

		txtCidade = new JTextField();
		txtCidade.setBounds(107, 175, 143, 19);
		contentPane.add(txtCidade);
		txtCidade.setColumns(10);

		JLabel lblNewLabel_4 = new JLabel("UF");
		lblNewLabel_4.setBounds(311, 178, 45, 13);
		contentPane.add(lblNewLabel_4);

		cbpUf = new JComboBox<>();
		cbpUf.setModel(new DefaultComboBoxModel<>(new String[] { "", "AC", "AL", "AP", "AM", "BA", "CE", "DF", "ES", "GO",
				"MA", "MT", "MS", "MG", "PA", "PB", "PR", "PE", "PI", "RJ", "RN", "RS", "RO", "RR", "SC", "SP", "SE", "TO" }));
		cbpUf.setBounds(337, 174, 65, 21);
		contentPane.add(cbpUf);

		JButton btnLimpar = new JButton("Limpar");
		btnLimpar.setBounds(57, 221, 85, 21);
		btnLimpar.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				txtCep.setText("");
				txtEndereco.setText("");
				txtBairro.setText("");
				txtCidade.setText("");
				cbpUf.setSelectedIndex(0);
				txtCep.requestFocus();
			}
		});
		contentPane.add(btnLimpar);

		JButton btnCEP = new JButton("Buscar");
		btnCEP.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				if (txtCep.getText().equals("")) {
					JOptionPane.showMessageDialog(null, "Informe o CEP");
					txtCep.requestFocus();
				} else {
					buscarCEP();
				}
			}
		});
		btnCEP.setBounds(271, 54, 85, 21);
		contentPane.add(btnCEP);

		JButton btnSobre = new JButton("");
		btnSobre.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				Sobre sobre = new Sobre();
				sobre.setVisible(true);
			}
		});
		btnSobre.setToolTipText("Sobre");
		btnSobre.setIcon(new ImageIcon(CEP.class.getResource("/img/info.png")));
		btnSobre.setCursor(Cursor.getPredefinedCursor(Cursor.HAND_CURSOR));
		btnSobre.setBackground(SystemColor.control);
		btnSobre.setBounds(378, 27, 48, 48);
		contentPane.add(btnSobre);

		txtCep.setDocument(new javax.swing.text.PlainDocument() {
			@Override
			public void insertString(int offs, String str, javax.swing.text.AttributeSet a)
					throws javax.swing.text.BadLocationException {
				if (str == null)
					return;
				if ((getLength() + str.length()) <= 8 && str.matches("\\d+")) {
					super.insertString(offs, str, a);
				}
			}
		});
	} // fim do construtor

	private void buscarCEP() {
		String cep = txtCep.getText();
		try {
			URL url = new URL("http://cep.republicavirtual.com.br/web_cep.php?cep=" + cep + "&formato=xml");
			SAXReader xml = new SAXReader();
			Document documento = xml.read(url);
			Element root = documento.getRootElement();

			String tipoLogradouro = root.elementText("tipo_logradouro");
			String logradouro = root.elementText("logradouro");
			String resultado = root.elementText("resultado");

			if ("1".equals(resultado)) {
				txtEndereco.setText(tipoLogradouro + " " + logradouro);
				txtBairro.setText(root.elementText("bairro"));
				txtCidade.setText(root.elementText("cidade"));
				cbpUf.setSelectedItem(root.elementText("uf"));
			} else {
				JOptionPane.showMessageDialog(null, "CEP não encontrado.");
			}
		} catch (Exception e) {
			JOptionPane.showMessageDialog(null, "Erro ao buscar CEP: " + e);
		}
	}
} // fim da classe
