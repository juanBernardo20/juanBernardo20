#include <iostream>
#include <iomanip>

// Function to determine if a year is a leap year
bool isLeapYear(int year) {
    return (year % 400 == 0) || ((year % 100 != 0) && (year % 4 == 0));
}

// Function to print a calendar for one year
void printCalendar(int year, int startDay) {
    const int DAYS_IN_MONTH[] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
    const std::string MONTH_NAMES[] = {"", "January", "February", "March", "April", "May", "June",
                                       "July", "August", "September", "October", "November", "December"};

    // Loop through each month
    for (int month = 1; month <= 12; ++month) {
        std::cout << "\n\t\t" << MONTH_NAMES[month] << "\n\n";
        std::cout << "  S  M  T  W  T  F  S\n---------------------\n";

        // Determine the number of days in the month, considering leap year for February
        int daysInMonth = DAYS_IN_MONTH[month];
        if (month == 2 && isLeapYear(year)) {
            daysInMonth = 29;
        }

        // Print leading spaces for the starting day
        for (int i = 0; i < startDay; ++i) {
            std::cout << std::setw(3) << " ";
        }

        // Print the days of the month
        for (int day = 1; day <= daysInMonth; ++day) {
            std::cout << std::setw(2) << day << " ";

            // Move to the next line after Saturday
            if ((startDay + day) % 7 == 0) {
                std::cout << "\n";
            }
        }

        // Update the starting day for the next month
        startDay = (startDay + daysInMonth) % 7;

        std::cout << "\n";
    }
}

int main() {
    int year, startDay;

    // Get input from the user
    std::cout << "What year do you want a calendar for? ";
    std::cin >> year;

    std::cout << "What day of the week does January 1 fall on? (Enter 0 for Sunday, 1 for Monday, etc.): ";
    std::cin >> startDay;

    // Print the calendar
    printCalendar(year, startDay);

    return 0;
}

PART THIS 
#include <iostream>
#include <iomanip>

// Function to determine if a year is a leap year
bool isLeapYear(int year) {
    return (year % 400 == 0) || ((year % 100 != 0) && (year % 4 == 0));
}

// Function to print a single month
void printMonth(int year, int month, int startDay) {
    const int DAYS_IN_WEEK = 7;
    const int DAYS_IN_MONTH[] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

    std::string monthNames[] = {"", "January", "February", "March", "April", "May", "June",
                                "July", "August", "September", "October", "November", "December"};

    // Print month header
    std::cout << std::setw(20) << year << "\n\n";
    std::cout << std::setw(20) << monthNames[month] << "\n\n";
    std::cout << std::setw(2) << "S " << "M T W T F S\n---------------------\n";

    // Calculate the number of days in the month, considering leap year for February
    int daysInMonth = DAYS_IN_MONTH[month];
    if (month == 2 && isLeapYear(year)) {
        daysInMonth = 29;
    }

    // Print the days of the month
    int day = 1;
    for (int i = 0; i < DAYS_IN_WEEK; ++i) {
        if (i < startDay) {
            std::cout << std::setw(2) << " ";
        } else {
            std::cout << std::setw(2) << day++;
        }
    }

    for (int i = startDay + 1; i < DAYS_IN_WEEK; ++i) {
        std::cout << std::setw(2) << day++;
    }

    std::cout << "\n";
    while (day <= daysInMonth) {
        for (int i = 0; i < DAYS_IN_WEEK && day <= daysInMonth; ++i) {
            std::cout << std::setw(2) << day++;
        }
        std::cout << "\n";
    }

    std::cout << "\n";
}

int main() {
    int year, startDay;

    // Get input from the user
    std::cout << "What year do you want a calendar for? ";
    std::cin >> year;

    std::cout << "What day of the week does January 1 fall on? (Enter 0 for Sunday, 1 for Monday, etc.): ";
    std::cin >> startDay;

    // Print the calendar for each month
    for (int month = 1; month <= 12; ++month) {
        printMonth(year, month, startDay);
        startDay = (startDay + 1) % 7; // Move to the next month
    }

    return 0;
}

