import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;

public class StudentInformationSystem {

    private JFrame mainFrame;
    private ArrayList<Student> studentList;
    private int currentStudentIndex = -1;

    public StudentInformationSystem() {
        studentList = new ArrayList<>();
        initialize();
    }

    private void initialize() {
        mainFrame = new JFrame("Оюутны мэдээллийн систем");
        mainFrame.setSize(600, 400);
        mainFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        mainFrame.setLocationRelativeTo(null);
        showMainMenu();
        mainFrame.setVisible(true);
    }

    private void showMainMenu() {
        mainFrame.getContentPane().removeAll();

        JPanel panel = new JPanel(new GridLayout(4, 1, 10, 10));
        JButton addStudentButton = new JButton("Оюутан нэмэх");
        JButton listStudentButton = new JButton("Оюутны жагсаалт");
        JButton exitButton = new JButton("Гарах");

        panel.add(addStudentButton);
        panel.add(listStudentButton);
        panel.add(exitButton);

        mainFrame.add(panel);

        addStudentButton.addActionListener(e -> showAddStudentScreen());
        listStudentButton.addActionListener(e -> showStudentListScreen());
        exitButton.addActionListener(e -> System.exit(0));

        mainFrame.revalidate();
        mainFrame.repaint();
    }

    private void showAddStudentScreen() {
        mainFrame.getContentPane().removeAll();

        JPanel panel = new JPanel(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(5, 5, 5, 5);
        gbc.anchor = GridBagConstraints.WEST;

        JLabel firstNameLabel = new JLabel("Нэр:");
        JTextField firstNameField = new JTextField(20);
        JLabel lastNameLabel = new JLabel("Овог:");
        JTextField lastNameField = new JTextField(20);
        JLabel emailLabel = new JLabel("Имэйл:");
        JTextField emailField = new JTextField(20);

        gbc.gridx = 0;
        gbc.gridy = 0;
        panel.add(firstNameLabel, gbc);
        gbc.gridx = 1;
        panel.add(firstNameField, gbc);

        gbc.gridx = 0;
        gbc.gridy = 1;
        panel.add(lastNameLabel, gbc);
        gbc.gridx = 1;
        panel.add(lastNameField, gbc);

        gbc.gridx = 0;
        gbc.gridy = 2;
        panel.add(emailLabel, gbc);
        gbc.gridx = 1;
        panel.add(emailField, gbc);

        JButton saveButton = new JButton("Хадгалах");
        JButton backButton = new JButton("Буцах");

        gbc.gridx = 0;
        gbc.gridy = 3;
        panel.add(saveButton, gbc);
        gbc.gridx = 1;
        panel.add(backButton, gbc);

        mainFrame.add(panel);

        saveButton.addActionListener(e -> {
            String firstName = firstNameField.getText().trim();
            String lastName = lastNameField.getText().trim();
            String email = emailField.getText().trim();

            if (firstName.isEmpty() || lastName.isEmpty() || email.isEmpty()) {
                JOptionPane.showMessageDialog(mainFrame, "Бүх талбарыг бөглөнө үү", "Алдаа", JOptionPane.ERROR_MESSAGE);
                return;
            }

            Student student = new Student(firstName, lastName, email);
            studentList.add(student);

            JOptionPane.showMessageDialog(mainFrame, "Оюутан амжилттай нэмэгдлээ.");
            showMainMenu();
        });

        backButton.addActionListener(e -> showMainMenu());

        mainFrame.revalidate();
        mainFrame.repaint();
    }

    private void showStudentListScreen() {
        mainFrame.getContentPane().removeAll();

        if (studentList.isEmpty()) {
            JOptionPane.showMessageDialog(mainFrame, "Одоогоор оюутан бүртгэлгүй байна.");
            showMainMenu();
            return;
        }

        String[] columnNames = {"Нэр", "Овог", "Имэйл"};
        String[][] data = new String[studentList.size()][3];

        for (int i = 0; i < studentList.size(); i++) {
            Student s = studentList.get(i);
            data[i][0] = s.getFirstName();
            data[i][1] = s.getLastName();
            data[i][2] = s.getEmail();
        }

        JTable table = new JTable(data, columnNames);
        table.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
        JScrollPane scrollPane = new JScrollPane(table);

        JButton detailsButton = new JButton("Дэлгэрэнгүй харах");
        JButton backButton = new JButton("Буцах");

        JPanel buttonPanel = new JPanel();
        buttonPanel.add(detailsButton);
        buttonPanel.add(backButton);

        mainFrame.setLayout(new BorderLayout());
        mainFrame.add(scrollPane, BorderLayout.CENTER);
        mainFrame.add(buttonPanel, BorderLayout.SOUTH);

        detailsButton.addActionListener(e -> {
            int selectedRow = table.getSelectedRow();
            if (selectedRow == -1) {
                JOptionPane.showMessageDialog(mainFrame, "Нэг оюутан сонгоно уу", "Анхааруулга", JOptionPane.WARNING_MESSAGE);
                return;
            }
            currentStudentIndex = selectedRow;
            showStudentDetailsScreen();
        });

        backButton.addActionListener(e -> showMainMenu());

        mainFrame.revalidate();
        mainFrame.repaint();
    }

    private void showStudentDetailsScreen() {
        mainFrame.getContentPane().removeAll();

        if (currentStudentIndex < 0 || currentStudentIndex >= studentList.size()) {
            JOptionPane.showMessageDialog(mainFrame, "Оюутан олдсонгүй");
            showStudentListScreen();
            return;
        }

        Student student = studentList.get(currentStudentIndex);

        JPanel detailsPanel = new JPanel(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(10, 10, 10, 10);
        gbc.anchor = GridBagConstraints.WEST;

        addDetailRow(detailsPanel, gbc, 0, "Нэр:", student.getFirstName());
        addDetailRow(detailsPanel, gbc, 1, "Овог:", student.getLastName());
        addDetailRow(detailsPanel, gbc, 2, "Имэйл:", student.getEmail());

        JPanel buttonPanel = new JPanel(new FlowLayout(FlowLayout.CENTER));
        JButton backButton = new JButton("Буцах");
        buttonPanel.add(backButton);

        mainFrame.setLayout(new BorderLayout());
        mainFrame.add(detailsPanel, BorderLayout.CENTER);
        mainFrame.add(buttonPanel, BorderLayout.SOUTH);

        backButton.addActionListener(e -> showStudentListScreen());

        mainFrame.revalidate();
        mainFrame.repaint();
    }

    // Туслах функц дэлгэрэнгүй талбар нэмэхэд
    private void addDetailRow(JPanel panel, GridBagConstraints gbc, int row, String label, String value) {
        gbc.gridx = 0;
        gbc.gridy = row;
        panel.add(new JLabel(label), gbc);

        gbc.gridx = 1;
        panel.add(new JLabel(value), gbc);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new StudentInformationSystem());
    }

    // Оюутны класс
    public static class Student {
        private String firstName;
        private String lastName;
        private String email;

        public Student(String firstName, String lastName, String email) {
            this.firstName = firstName;
            this.lastName = lastName;
            this.email = email;
        }

        public String getFirstName() { return firstName; }
        public String getLastName() { return lastName; }
        public String getEmail() { return email; }
    }
}
