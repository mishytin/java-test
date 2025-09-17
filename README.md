# java
Архангельский Михаил

import java.util.*;

public class game {
    public static void main(String[] args) {
        String[] words = {"cenla", "java"};
        Random rand = new Random();
        String word = words[rand.nextInt(words.length)];
        Set<Character> guessedLetters = new HashSet<>();
        int lives = 6;

        Scanner scanner = new Scanner(System.in);

        while (lives > 0) {
            //с пропусками
            String displayWord = "";
            boolean guessedAll = true;
            for (int i = 0; i < word.length(); i++) {
                char c = word.charAt(i);
                if (guessedLetters.contains(c)) {
                    displayWord += c + " ";
                } else {
                    displayWord += "_ ";
                    guessedAll = false;
                }
            }
            System.out.println("Слово: " + displayWord);
            System.out.println("Жизни: " + lives);
            System.out.print("Введите букву: ");
            String input = scanner.nextLine().toLowerCase();

            if (input.length() != 1 || !Character.isLetter(input.charAt(0))) {
                System.out.println("Пожалуйста, введите одну букву");
                continue;
            }

            char guess = input.charAt(0);
            if (guessedLetters.contains(guess)) {
                System.out.println("Эта буква уже была");
                continue;
            }

            guessedLetters.add(guess);

            if (word.indexOf(guess) >= 0) {
                System.out.println("Правильно!");
            } else {
                lives--;
                System.out.println("Неверно!");
            }

            if (guessedAll) {
                System.out.println("Поздравляю! Вы угадали слово: " + word);
                break;
            }
        }

        if (lives == 0) {
            System.out.println("Вы проиграли! Загаданное слово было: " + word);
        }

        scanner.close();
    }
}
