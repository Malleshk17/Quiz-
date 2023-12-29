import java.util.Scanner;

public class QuizApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Create a Quiz instance and add questions
        Quiz quiz = new Quiz();
        quiz.addQuestion(new Question("What is the capital of France?", new String[]{"Berlin", "Paris", "Madrid"}, 1));
        quiz.addQuestion(new Question("Which planet is known as the Red Planet?", new String[]{"Mars", "Jupiter", "Venus"}, 0));

        // User interaction loop
        int score = 0;
        for (int i = 0; i < quiz.getQuizSize(); i++) {
            Question currentQuestion = quiz.getQuestion(i);

            // Display the question
            System.out.println("Question " + (i + 1) + ": " + currentQuestion.getQuestionText());
            
            // Display answer options
            String[] options = currentQuestion.getOptions();
            for (int j = 0; j < options.length; j++) {
                System.out.println((j + 1) + ". " + options[j]);
            }

            // Get and validate user input
            int userAnswer;
            do {
                System.out.print("Your answer (1-" + options.length + "): ");
                while (!scanner.hasNextInt()) {
                    System.out.println("Invalid input. Please enter a number.");
                    scanner.next(); // consume the invalid input
                }
                userAnswer = scanner.nextInt();
            } while (userAnswer < 1 || userAnswer > options.length);

            // Check if the user's answer is correct
            if (userAnswer - 1 == currentQuestion.getCorrectAnswerIndex()) {
                System.out.println("Correct!\n");
                score++;
            } else {
                System.out.println("Incorrect. The correct answer is " + options[currentQuestion.getCorrectAnswerIndex()] + "\n");
            }
        }

        // Display final score
        System.out.println("Quiz completed! Your score: " + score + " out of " + quiz.getQuizSize());

        // Close the scanner
        scanner.close();
    }
}
