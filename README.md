import java.util.*;

class Quiz {
    private String topic;
    private List<Question> questions;

    public Quiz(String topic) {
        this.topic = topic;
        this.questions = new ArrayList<>();
    }

    public void addQuestion(Question question) {
        questions.add(question);
    }

    public String getTopic() {
        return topic;
    }

    public List<Question> getQuestions() {
        return questions;
    }
}

class Question {
    private String question;
    private String answer;

    public Question(String question, String answer) {
        this.question = question;
        this.answer = answer;
    }

    public String getQuestion() {
        return question;
    }

    public String getAnswer() {
        return answer;
    }
}

public class QuizApplication {
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        // Create quizzes
        Quiz javaQuiz = new Quiz("Java Basics");
        javaQuiz.addQuestion(new Question("What is the capital of Japan?", "Tokyo"));
        javaQuiz.addQuestion(new Question("What is 2 + 2?", "4"));

        Quiz scienceQuiz = new Quiz("Science Trivia");
        scienceQuiz.addQuestion(new Question("What is the chemical symbol for water?", "H2O"));
        scienceQuiz.addQuestion(new Question("What planet is known as the Red Planet?", "Mars"));

        // Present quizzes to the user
        List<Quiz> quizzes = Arrays.asList(javaQuiz, scienceQuiz);
        presentQuizzes(quizzes);

        // Allow user to select a quiz
        int selectedQuizIndex = getSelectedQuizIndex(quizzes.size());
        Quiz selectedQuiz = quizzes.get(selectedQuizIndex);

        // Take the selected quiz
        takeQuiz(selectedQuiz);
    }

    private static void presentQuizzes(List<Quiz> quizzes) {
        System.out.println("Welcome to the Quiz Application!\n");
        System.out.println("Available Quizzes:");
        for (int i = 0; i < quizzes.size(); i++) {
            System.out.println((i + 1) + ". " + quizzes.get(i).getTopic());
        }
    }

    private static int getSelectedQuizIndex(int numQuizzes) {
        int selectedQuizIndex;
        do {
            System.out.print("\nSelect a quiz (1-" + numQuizzes + "): ");
            selectedQuizIndex = scanner.nextInt();
            if (selectedQuizIndex < 1 || selectedQuizIndex > numQuizzes) {
                System.out.println("Invalid input. Please enter a number between 1 and " + numQuizzes + ".");
            }
        } while (selectedQuizIndex < 1 || selectedQuizIndex > numQuizzes);
        return selectedQuizIndex - 1;
    }

    private static void takeQuiz(Quiz quiz) {
        System.out.println("\n--- " + quiz.getTopic() + " ---");
        List<Question> questions = quiz.getQuestions();
        int score = 0;

        for (int i = 0; i < questions.size(); i++) {
            Question question = questions.get(i);
            System.out.println("\nQuestion " + (i + 1) + ": " + question.getQuestion());
            System.out.print("Your answer: ");
            String userAnswer = scanner.next().trim();

            if (userAnswer.equalsIgnoreCase(question.getAnswer())) {
                System.out.println("Correct!");
                score++;
            } else {
                System.out.println("Incorrect. The correct answer is: " + question.getAnswer());
            }
        }

        System.out.println("\nQuiz complete!");
        System.out.println("Your score: " + score + "/" + questions.size());
    }
}

