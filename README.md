import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SimpleJavaQuizApp extends JFrame implements ActionListener {
    private JLabel questionLabel;
    private JRadioButton[] options;
    private ButtonGroup optionsGroup;
    private JButton nextButton;
    private int currentQuestionIndex = 0;
    private int score = 0;

    private String[][] questions = {
        {"Which of the following is not a Java feature?", "Object-oriented", "Use of pointers", "Portable", "Dynamic", "1"},
        {"What is the extension of Java code files?", ".js", ".txt", ".class", ".java", "3"},
        {"Which method is the entry point for a Java program?", "main()", "start()", "begin()", "init()", "0"},
        {"Which of these cannot be used for a variable name in Java?", "identifier", "keyword", "variable", "constant", "1"},
        {"What is the size of an int variable in Java?", "4 bytes", "8 bytes", "2 bytes", "16 bytes", "0"},
        {"Which of the following is a reserved keyword in Java?", "object", "strictfp", "main", "system", "1"},
        {"Which of these operators is used to allocate memory for an object?", "malloc", "alloc", "new", "create", "2"},
        {"Which keyword is used for accessing the features of a package?", "package", "import", "extends", "implements", "1"},
        {"Which of these is a superclass of all exceptions in Java?", "RuntimeException", "Exception", "Throwable", "Error", "2"},
        {"What is the default value of a boolean variable in Java?", "true", "false", "0", "1", "1"}
    };

    public SimpleJavaQuizApp() {
        setTitle("Java Quiz App");
        setSize(500, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(null);

        questionLabel = new JLabel();
        questionLabel.setBounds(50, 50, 400, 30);
        add(questionLabel);

        options = new JRadioButton[4];
        optionsGroup = new ButtonGroup();
        for (int i = 0; i < 4; i++) {
            options[i] = new JRadioButton();
            options[i].setBounds(50, 100 + (i * 40), 400, 30);
            optionsGroup.add(options[i]);
            add(options[i]);
        }

        nextButton = new JButton("Next");
        nextButton.setBounds(200, 300, 100, 30);
        nextButton.addActionListener(this);
        add(nextButton);

        loadQuestion();
        setVisible(true);
    }

    private void loadQuestion() {
        if (currentQuestionIndex < questions.length) {
            questionLabel.setText(questions[currentQuestionIndex][0]);
            for (int i = 0; i < 4; i++) {
                options[i].setText(questions[currentQuestionIndex][i + 1]);
                options[i].setSelected(false);
            }
        } else {
            showResult();
        }
    }

    private void showResult() {
        JOptionPane.showMessageDialog(this, "Your score is: " + score + "/" + questions.length);
        System.exit(0);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        if (getSelectedOption() == Integer.parseInt(questions[currentQuestionIndex][5])) {
            score++;
        }
        currentQuestionIndex++;
        loadQuestion();
    }

    private int getSelectedOption() {
        for (int i = 0; i < 4; i++) {
            if (options[i].isSelected()) {
                return i;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        new SimpleJavaQuizApp();
    }
}
