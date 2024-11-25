#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_INPUT_LENGTH 100
#define SPEED_THRESHOLD 100.0 
#define MAX_TIME_LENGTH 10

typedef struct TrafficRecord {
    char time[MAX_TIME_LENGTH];
    int vehicles;
    float speed;
    struct TrafficRecord *next;
} TrafficRecord;

void addRecord(TrafficRecord **head);
void displaySummary(TrafficRecord *head);
void calculateAverageSpeed(TrafficRecord *head);
void calculateTotalVehicles(TrafficRecord *head);
void detectSecurityThreats(TrafficRecord *head);

int main() {
    TrafficRecord *head = NULL;
    char command[MAX_INPUT_LENGTH];

    while (1) {
        printf("Enter command (1.add, 2.avg_speed, 3.total_vehicles, 4.detect_threats,5.quit): ");
        scanf("%s", command);

        if (strcmp(command, "1") == 0) {
            addRecord(&head);
        } else if (strcmp(command, "2") == 0) {
            calculateAverageSpeed(head);
        } else if (strcmp(command, "3") == 0) {
            calculateTotalVehicles(head);
        } else if (strcmp(command, "4") == 0) {
            detectSecurityThreats(head);
        } else if (strcmp(command, "5") == 0) {
            break;
        } else {
            printf("Unknown command. Please try again.\n");
        }
    }

    TrafficRecord *current = head;
    TrafficRecord *next;
    while (current != NULL) {
        next = current->next;
        free(current);
        current = next;
    }

    return 0;
}

void addRecord(TrafficRecord **head) {
    TrafficRecord *newRecord = (TrafficRecord *)malloc(sizeof(TrafficRecord));
    if (newRecord == NULL) {
        printf("Memory allocation failed.\n");
        return;
    }

    printf("Enter time (HH:MM): ");
    scanf("%s", newRecord->time);
    printf("Enter number of vehicles: ");
    scanf("%d", &newRecord->vehicles);
    printf("Enter average speed: ");
    scanf("%f", &newRecord->speed);

}

