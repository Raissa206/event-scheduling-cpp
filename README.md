# event-scheduling-cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <sstream>

using namespace std;

// Class representing a single Event
class Event {
public:
    string name;
    string date;
    string time;

    // Default constructor
    Event() {}

    // Parameterized constructor
    Event(string n, string d, string t) : name(n), date(d), time(t) {}

    // Converts event data to a single string for file storage
    string toString() const {
        return name + "|" + date + "|" + time;
    }

    // Creates an Event object from a string (read from file)
    static Event fromString(const string& line) {
        stringstream ss(line);
        string n, d, t;
        getline(ss, n, '|');  // Get name
        getline(ss, d, '|');  // Get date
        getline(ss, t, '|');  // Get time
        return Event(n, d, t);
    }

    // Displays the event details
    void display() const {
        cout << "Event: " << name << ", Date: " << date << ", Time: " << time << endl;
    }
};

// Class responsible for managing events (add, view, delete)
class Scheduler {
    string filename = "events.txt";  // File to store event data

public:
    // Adds an event to the file
    void addEvent(const Event& e) {
        ofstream file(filename, ios::app);  // Open file in append mode
        if (file.is_open()) {
            file << e.toString() << endl;  // Write event to file
            file.close();
            cout << "Event added successfully!\n";
        } else {
            cout << "Error opening file.\n";
        }
    }

    // Loads all events from the file into a vector
    vector<Event> loadEvents() {
        vector<Event> events;
        ifstream file(filename);
        string line;

        if (file.is_open()) {
            while (getline(file, line)) {
                if (!line.empty()) {
                    events.push_back(Event::fromString(line));  // Convert string to Event
                }
            }
            file.close();
        }
        return events;
    }

    // Displays all events to the user
    void viewEvents() {
        vector<Event> events = loadEvents();
        if (events.empty()) {
            cout << "No events found.\n";
        } else {
            for (const auto& e : events) {
                e.display();  // Print each event
            }
        }
    }

    // Deletes an event by name
    void deleteEvent(const string& nameToDelete) {
        vector<Event> events = loadEvents();
        ofstream file(filename);  // Overwrite file
        bool found = false;

        for (const auto& e : events) {
            if (e.name != nameToDelete) {
                file << e.toString() << endl;  // Keep other events
            } else {
                found = true;  // Found the event to delete
            }
        }

        file.close();
        if (found)
            cout << "Event deleted.\n";
        else
            cout << "Event not found.\n";
    }
};

// Main function: User Interface
int main() {
    Scheduler scheduler;
    int choice;

    do {
        // Display menu
        cout << "\n--- Event Scheduler ---\n";
        cout << "1. Add Event\n";
        cout << "2. View Events\n";
        cout << "3. Delete Event\n";
        cout << "0. Exit\n";
        cout << "Choose an option: ";
        cin >> choice;

        cin.ignore(); // Ignore leftover newline to avoid input issues

        // Process user choice
        if (choice == 1) {
            string name, date, time;
            cout << "Enter event name: ";
            getline(cin, name);
            cout << "Enter date (YYYY-MM-DD): ";
            getline(cin, date);
            cout << "Enter time (HH:MM): ";
            getline(cin, time);
            scheduler.addEvent(Event(name, date, time));
        } else if (choice == 2) {
            scheduler.viewEvents();
        } else if (choice == 3) {
            string name;
            cout << "Enter event name to delete: ";
            getline(cin, name);
            scheduler.deleteEvent(name);
        }

    } while (choice != 0);  // Repeat until user exits

    return 0;
}
