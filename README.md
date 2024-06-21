import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

// Class to represent a Quiz Question
class Question {
    private String questionText;
    private List<String> options;
    private String correctAnswer;

    public Question(String questionText, List<String> options, String correctAnswer) {
        this.questionText = questionText;
        this.options = options;
        this.correctAnswer = correctAnswer;
    }

    public String getQuestionText() {
        return questionText;
    }

    public List<String> getOptions() {
        return options;
    }

    public String getCorrectAnswer() {
        return correctAnswer;
    }
}

// Main Quiz Application class
public class QuizApplication {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Create questions
        List<Question> questions = new ArrayList<>();
        questions.add(new Question("What is the capital of France?", List.of("London", "Paris", "Berlin", "Madrid"), "Paris"));
        questions.add(new Question("Who wrote 'Romeo and Juliet'?", List.of("Jane Austen", "Charles Dickens", "William Shakespeare", "Mark Twain"), "William Shakespeare"));
        questions.add(new Question("What is the largest mammal?", List.of("Elephant", "Blue whale", "Giraffe", "Polar bear"), "Blue whale"));

        int score = 0;

        // Quiz loop
        for (int i = 0; i < questions.size(); i++) {
            Question q = questions.get(i);
            System.out.println("Question " + (i + 1) + ": " + q.getQuestionText());
            
            // Display options
            List<String> options = q.getOptions();
            for (int j = 0; j < options.size(); j++) {
                System.out.println((j + 1) + ". " + options.get(j));
            }

            // User input
            System.out.print("Enter your answer (1-" + options.size() + "): ");
            int userAnswerIndex = scanner.nextInt();
            scanner.nextLine(); // Consume newline left-over

            // Validate answer
            if (userAnswerIndex >= 1 && userAnswerIndex <= options.size()) {
                String userAnswer = options.get(userAnswerIndex - 1);
                if (userAnswer.equalsIgnoreCase(q.getCorrectAnswer())) {
                    System.out.println("Correct!\n");
                    score++;
                } else {
                    System.out.println("Incorrect. The correct answer is: " + q.getCorrectAnswer() + "\n");
                }
            } else {
                System.out.println("Invalid input. Skipping question...\n");
            }
        }

        // Quiz complete
        System.out.println("Quiz complete!");
        System.out.println("Your score is: " + score + " out of " + questions.size());

        scanner.close();
    }
}
