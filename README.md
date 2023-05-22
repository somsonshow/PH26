public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Введите Pmin.вкл: ");
        double pMinVkl = readDouble(scanner);

        // Расчеты по формулам
        double pMaxPad = pMinVkl / 3;
        double pKontVyx = pMinVkl - pMaxPad;
        double deltaT = pMaxPad * 6.8 / 45;
        double tVkl = convertTime(scanner, "Введите время включения (в формате ЧЧ:ММ): ");
        double tVyx = tVkl + deltaT;
        double tObsch = pMinVkl * 6.8 / 45;
        double tVozvr = tVkl + tObsch;

        // Вывод результатов
        System.out.println("Pmax.пад: " + pMaxPad + " бар");
        System.out.println("Pк.вых: " + pKontVyx + " бар");
        System.out.println("ΔT: " + deltaT + " мин");
        System.out.println("Tвых: " + convertToTimeFormat(tVyx));
        System.out.println("Tобщ: " + tObsch + " мин");
        System.out.println("Tвозвр: " + convertToTimeFormat(tVozvr));
    }

    private static double readDouble(Scanner scanner) {
        double value;
        while (true) {
            try {
                value = scanner.nextDouble();
                break;
            } catch (Exception e) {
                System.out.println("Ошибка: введите числовое значение.");
                scanner.nextLine(); // Очистка буфера ввода
            }
        }
        return value;
    }

    private static double convertTime(Scanner scanner, String prompt) {
        double time;
        while (true) {
            System.out.print(prompt);
            String input = scanner.next();
            if (input.matches("\\d{2}:\\d{2}")) {
                String[] parts = input.split(":");
                int hours = Integer.parseInt(parts[0]);
                int minutes = Integer.parseInt(parts[1]);
                time = hours * 60 + minutes;
                break;
            } else {
                System.out.println("Ошибка: некорректный формат времени. Введите время в формате ЧЧ:ММ.");
            }
        }
        return time;
    }

    private static String convertToTimeFormat(double minutes) {
        int hours = (int) minutes / 60;
        int mins = (int) minutes % 60;
        return String.format("%02d:%02d", hours, mins);
    }
}
