📅 Event Scheduling System (C++ File Handling Project)
🔍 Project Overview
This is a simple Event Scheduling System developed in C++, utilizing Object-Oriented Programming (OOP) principles and file handling. It allows users to create, view, search, update, and delete events. All event data is stored and retrieved from a text file, demonstrating persistent data storage without a database.
💡 Features
📌 Add new events with date, time, and description
📋 View all scheduled events
🔍 Search events by date
✏️ Update event details
❌ Delete events
💾 File-based storage for event persistence
🧱 Uses core OOP principles: Classes, Inheritance, Encapsulation
🛠️ Technologies Used
Language: C++
File Handling: fstream (read/write operations)
Environment: Console Application
📂 File Structure
EventScheduler/
│
├── main.cpp             # Main program file
├── EventScheduler.txt   # Text file to store event data
├── README.md            # Project documentation
🧱 OOP Concepts Applied
Concept	Description
Class	Event class encapsulates event details.
Encapsulation	Getters and setters protect class attributes.
File Handling	Stores and retrieves data from .txt file.
Modularity	Functions for each task (add, update, delete, etc.).
🚀 How to Run
1. Clone or Download this repository
2. Open in any C++ IDE (Code::Blocks, Dev C++, Visual Studio, etc.)
3. Compile the main.cpp file
4. Run the executable in a console
📝 Sample Event Format in File
Each event is stored in the following format in the EventScheduler.txt file:
Event ID: 1
Title: Meeting with Team
Date: 2025-06-30
Time: 10:00 AM
Description: Discuss project milestones.
✅ Future Enhancements
Add login system (admin/user roles)
Use of binary file storage for better performance
Export events to .csv format
Add support for reminders/notifications
🧠 Challenges Faced
Ensuring unique event IDs and clean file updates
Managing file rewriting during delete/update operations
Avoiding data corruption during concurrent file access
📚 License
This project is open-source and free to use for educational purposes 😉 
🙋‍♂️ Author
Lankoko Ayinda Raïssa 
