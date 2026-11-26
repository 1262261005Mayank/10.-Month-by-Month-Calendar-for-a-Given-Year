# 10.-Month-by-Month-Calendar-for-a-Given-Year
#include <stdio.h>
#include <time.h>

int isLeapYear(int year) {
    return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
}

int getFirstDayOfYear(int year) {
    struct tm time_in = {0};
    time_in.tm_year = year - 1900;
    time_in.tm_mon = 0;
    time_in.tm_mday = 1;
    mktime(&time_in);
    return time_in.tm_wday; // 0 = Sunday, 6 = Saturday
}

int main() {
    int year, m, d, startDay;
    const char *months[] = {
        "January", "February", "March", "April", "May", "June",
        "July", "August", "September", "October", "November", "December"
    };
    int daysInMonth[] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

    printf("Enter the year: ");
    scanf("%d", &year);

    if (isLeapYear(year)) {
        daysInMonth[1] = 29;
    }

    startDay = getFirstDayOfYear(year);

    for (m = 0; m < 12; m++) {
        printf("\n  ------------ %s %d ------------\n", months[m], year);
        printf("  Sun  Mon  Tue  Wed  Thu  Fri  Sat\n");

        for (int space = 0; space < startDay; space++) {
            printf("     ");
        }

        for (d = 1; d <= daysInMonth[m]; d++) {
            printf("%5d", d);
            if ((startDay + d) % 7 == 0) {
                printf("\n");
            }
        }
        printf("\n");
        startDay = (startDay + daysInMonth[m]) % 7;
    }

    return 0;
}
