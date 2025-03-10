

# Movie Ticket Booking System

## Project Description
The **Movie Ticket Booking System** is a console-based C++ application that allows users to manage movie tickets and theater information. It provides a text-based menu interface where users can register their profiles, browse available movies, check seat availability, and book tickets. The system uses linked list data structures to maintain lists of users and movies, enabling efficient insertion and removal of records. This project demonstrates fundamental use of data structures (like linked lists, stacks, and queues), file handling for data persistence, and basic exception handling to create a robust and user-friendly experience.

## Features
- **User Registration and Profile Management**: Users can create a new account by entering details (username, age, balance). The application stores user profiles and allows viewing the current user's information at any time.
- **Movie Listing and Catalog Management**: View a list of all available movies along with their details (name, duration, genre, rating, ticket price, seats available). Authorized users (developers) can add new movies to the catalog, edit existing movie details, or delete movies.
- **Seat Booking and Availability Check**: Book tickets for a selected movie by specifying the number of seats to reserve. The system checks if the requested number of seats are available before confirming the booking, then updates the number of booked seats. Users can also display a seating chart for a movie to see which seats are free or already booked.
- **File Handling for Records**: User profiles and ticket bookings are saved to text files (e.g., `userprofile.txt` for users and `ticket.txt` for tickets). This allows the program to persist data between runs. Users can view saved profile information or tickets from these files through menu options.
- **Exception Handling**: The program includes try/catch blocks and input validation to handle errors gracefully. Invalid inputs (like wrong data types) or runtime exceptions are caught and an error message is displayed instead of crashing, improving the overall user experience.

## Technologies Used
- **C++** – Core programming language used to build the application (using C++17 features and Standard Library).
- **Data Structures** – **Linked lists** to store collections of users and movies. The user list is managed as a stack (LIFO) structure, and movie additions use a queue-like (FIFO) approach. **Stack** and **Queue** concepts are implemented for managing these lists.
- **File Handling** – Use of file streams (`<fstream>`) to read and write data to text files for persistent storage of user profiles and tickets.
- **Algorithms** – A merge sort algorithm is implemented to sort the movies alphabetically before displaying the list to the user.
- **Exception Handling** – Use of C++ exception handling (`try`, `catch`, `std::exception`) to manage invalid input and other runtime errors.

## Installation Instructions
1. **Prerequisites**: Make sure you have a C++ compiler installed on your system (for example, GCC/G++ for Linux/Mac or MS Visual C++ for Windows). No additional libraries are required beyond the C++ Standard Library.
2. **Clone or Download** the project source code from the repository.
3. **Compile the project**:
   - **Using G++ (Linux/Mac)**: Open a terminal in the project directory and compile the code with:  
     ```bash
     g++ -std=c++17 -o MovieTicketBookingSystem DSAPROJECT.cpp
     ``` 
     This will produce an executable named `MovieTicketBookingSystem`.
   - **Using Visual Studio (Windows)**: Open the project in Visual Studio (or create a new C++ console project and add the source file). Then build the solution. Ensure that you enable C++17 (or a compatible standard) in project settings.
   - *Note*: The code uses `<windows.h>` for console color settings. If you are compiling on a non-Windows system, you may need to remove or comment out Windows-specific calls (like `system("color 70")`) as they are not essential for core functionality.
4. **Run the application**:
   - If compiled from the terminal, run the executable: `./MovieTicketBookingSystem` (Linux/Mac) or `MovieTicketBookingSystem.exe` (Windows).
   - If using an IDE like Visual Studio, run the project through the IDE (e.g., "Start without debugging" in Visual Studio).
5. You should see the console interface with the main menu once the program is running.

## Usage Guide
After launching the program, an introduction banner/pattern is displayed, followed by a **menu** of options. Navigate the menu by entering the number corresponding to the desired action. Below is an overview of the available operations:

- **1. Book Ticket** – Start the ticket booking process. You will be prompted to select a movie and enter the number of seats to book. The system will verify availability and confirm the booking, then save the ticket information to the file.
- **2. Show Movies List** – Display all movies currently available in the system, sorted in alphabetical order by title. For each movie, details like duration, genre, rating, ticket price, total seats, and seats booked are shown.
- **3. Check Seats** – Check seat availability for a specific movie. You will be asked to enter the movie name, and the program will display a seat map (e.g., `0` for available seats and `X` for booked seats) so you can visualize which seats are still free.
- **4. Show Ticket** – View all booked ticket records. The program will read from the `ticket.txt` file and display the tickets that have been booked (including movie names and number of seats booked).
- **5. UserProfile** – Display the current user's profile information (username, age, balance) as recorded in the `userprofile.txt` file.
- **6. Add Movie** – *(Developer option)* Add a new movie to the movie list. You will be prompted to enter the movie’s details (name, duration, number of seats, rating, genre, price). The new movie will be appended to the movie list.
- **7. Edit Movie** – *(Developer option)* Modify the details of an existing movie. You will enter the name of the movie to edit, and then provide new information for that movie (duration, seats, rating, etc.). The movie’s record will be updated accordingly.
- **8. Delete Movie** – *(Developer option)* Remove a movie from the catalog. After entering the name of the movie to delete, that movie will be removed from the linked list of movies.
- **9. Sort the Movies** – *(Developer option)* Manually trigger sorting of the movie list in alphabetical order. *(Note: The "Show Movies List" option automatically sorts the list as well, so this option is mainly for demonstration.)*
- **0. Exit** – Quit the application. The program will save any new records (if not already saved) and terminate.

When interacting with the application, follow the on-screen prompts. Input data as requested (e.g., entering names or numbers). The program will guide you if an invalid input is detected (thanks to the validation and exception handling).

## Code Structure
The project is organized into logical components, using structured data types and classes to handle different aspects of the system:

- **Data Models (Structs)**:  
  - `User` – stores user information such as `username`, `age`, and `moneyBalance` (account balance).  
  - `Movie` – stores movie details including `name`, `duration` (in minutes), total `seats`, number of `seatsBooked`, `rating`, `genre`, and `price` (ticket price).  
  - `Node_User` – a node in the linked list of users. Contains a `User` object and a pointer to the next node (used to build a stack of users).  
  - `Node_Movie` – a node in the linked list of movies. Contains a `Movie` object and a pointer to the next node (used to link all movies in the catalog).
- **Classes**:  
  - `UserList` – Manages a collection of users in a stack-like structure (LIFO). Internally, it uses `Node_User` nodes linked together. Key functions include:
    - `pushUser(User u)` to add a new user to the stack (top of list).
    - `popUser()` to remove the most recently added user (if needed).
    - `displayUserInfo()` to show the current user's information on the console.
  - `MovieList` – Manages the linked list of movies (like a queue for additions). Internally uses `Node_Movie` nodes. Key functions include:
    - `addMovie(Movie m)` to add a new movie to the end of the list (FIFO addition).
    - `dequeueMovie()` to remove the movie at the front of the list (used if implementing a queue behavior).
    - `displayMoviesAlphabetically()` to sort the movies (using merge sort internally) and display them in order.
    - `displaySeats(const Movie& m)` to output a formatted seat map for a given movie, showing available vs. booked seats.
    - `bookSeats(Movie &m, int numSeats)` to attempt to book a given number of seats for movie `m` (updates `seatsBooked` if enough seats are available).
    - `findMovie(const std::string &name)` to search for a movie in the list by its name (returns a pointer to the movie node, used for editing or deleting).
    - `editMovie(const std::string &name, const Movie &newData)` to update the details of a movie identified by name.
    - `deleteMovie(const std::string &name)` to remove a movie from the list by title.
    - *Internal:* `mergeSortMovies()` (with helper `mergeSortedLists()`) to sort the movie nodes alphabetically by title.
- **Functions** (outside classes):  
  - `createUser()` – prompts the console user for input and creates a new `User` object (used during registration).
  - `writeUserToFile(const User& u)` – saves a user's information to "userprofile.txt" (appends to the file).
  - `displayUserProfileFromFile()` – reads and displays all user profile entries from "userprofile.txt".
  - `bookTicket(UserList &ul, MovieList &ml)` – coordinates the process of booking a ticket: it asks which movie to book and how many seats, then uses `MovieList::bookSeats` and records the transaction in "ticket.txt".
  - `checkSeats(const MovieList &ml)` – asks for a movie name and uses `MovieList::displaySeats` to show the seat availability for that movie.
  - `editMovie(MovieList &ml)` – interacts with the user to get a movie name and new details, then calls `MovieList::editMovie`.
  - `deleteMovie(MovieList &ml)` – gets a movie name from the user and calls `MovieList::deleteMovie` to remove it.
  - `showTicket()` – reads from "ticket.txt" and prints out all booked ticket records (movie name and number of seats booked).
  - `displayMenu(UserList &ul, MovieList &ml)` – the main menu loop function that displays all available options (as described in the Usage Guide) and invokes the appropriate functionality based on user choice. It also contains error handling for invalid inputs.
  - `EntryPattern()` – a utility function that prints a decorative intro pattern on program start (for visual flair).
- **Main Function** (`main()` in *DSAPROJECT.cpp*): The entry point of the application. In `main()`, the program initializes the data structures and pre-loads some initial movies into the `MovieList`. It may also prompt for an initial user or perform any required startup routines. Then it calls `EntryPattern()` to display the intro banner and begins the main loop by invoking `displayMenu(userList, movieList)`. The `main` function ties together all components, maintaining the `UserList` (current user context) and `MovieList` (movie catalog) throughout the program execution.


