# GOALBUDDY
#### Video Demo:  <https://youtu.be/AUeGPPyy3uI?si=umQ_6mvELMW1Mhiv>
#### Description:
**GoalBuddy: A Smart Goal-Tracking iOS App**  
GoalBuddy is a SwiftUI-based iOS application designed to help users set, track, and manage their goals efficiently. The app allows users to add, edit, and delete goals while also marking them as complete. To improve organization, goals are grouped by month, making it easier for users to track their progress over time. The app ensures data persistence using `UserDefaults`, allowing users to retain their goals even after closing and reopening the app.  

The development of GoalBuddy required thoughtful consideration of design choices, from structuring the data model to implementing interactive UI elements like swipe gestures for deletion. The core functionality revolves around four main Swift files: `Goal.swift`, `GoalViewModel.swift`, `ContentView.swift`, and `EditGoalView.swift`, each playing a distinct role in managing and displaying the goals effectively.  

**The Data Model: Structuring Goals**  
At the heart of GoalBuddy is `Goal.swift`, which defines the data model for a goal. Each goal consists of a unique identifier (`UUID`), a title, a description, a deadline, and a Boolean flag to indicate whether the goal is completed. The struct conforms to `Codable`, making it easy to store and retrieve goals from persistent storage.  

The decision to include an explicit `isCompleted` flag instead of inferring completion based on the deadline was deliberate. Users may want to track goals they have finished ahead of time, and a dedicated field provides flexibility in handling completion status.  

**Managing Goals: The ViewModel Approach**  
The `GoalViewModel.swift` file manages the core logic for adding, updating, deleting, and organizing goals. As an `ObservableObject`, it ensures that changes to the goal list are automatically reflected in the UI. The `@Published` property wrapper is used to trigger updates whenever goals are modified.  

One of the key features of the ViewModel is grouping goals by month. This is achieved by using a `DateFormatter` to extract the month and year from each goal's deadline and grouping the goals accordingly in a dictionary. This structured approach allows for easy navigation and better visualization of upcoming and past goals.  

Another crucial aspect of the ViewModel is data persistence. Goals are saved using `UserDefaults`, ensuring that they are not lost when the app is closed. When the app launches, the ViewModel loads stored goals from `UserDefaults` and decodes them back into the `Goal` structure. While `UserDefaults` is a simple and effective storage solution, a more scalable approach like `Core Data` could be considered for future versions if additional features such as sorting, filtering, or syncing across devices are required.  

**Building the User Interface: The Main Content View**  
The main interface, implemented in `ContentView.swift`, displays goals grouped by month. A `List` view dynamically updates to reflect any changes in the ViewModel. Each goal is represented with a checkbox for marking it as complete, along with its title, description, and deadline. The text color and strikethrough style adjust based on the goal's completion status, providing clear visual feedback to the user.  

A key interactive feature is the swipe-to-delete functionality. Users can remove a goal by swiping left, a common gesture in iOS apps that improves usability. Additionally, tapping a goal opens an edit screen, allowing users to modify details such as the title, description, or deadline.  

**Editing Goals: A Separate View for Flexibility**  
The ability to edit goals is implemented in `EditGoalView.swift`. This view allows users to update goal details using a `Form` containing `TextField` elements for the title and description, along with a `DatePicker` for selecting the deadline. When the user saves their changes, the ViewModel updates the corresponding goal in the list.  

To enhance usability, the editing screen opens as a modal sheet. This keeps the user experience smooth and consistent with common iOS design patterns. The environment property `@Environment(\.presentationMode)` is used to dismiss the edit view once the changes are saved, providing a seamless transition back to the main list.  

**Challenges and Design Decisions**  
Throughout the development process, several design decisions were carefully considered. One major debate was the choice between `UserDefaults` and `Core Data` for data persistence. While `UserDefaults` offers a simple solution for small datasets, it is not ideal for handling large amounts of data efficiently. Given the app's current scope, `UserDefaults` was sufficient, but transitioning to `Core Data` or CloudKit in the future could enhance functionality.  

Another design consideration was whether to allow users to categorize goals manually or automatically group them by deadline. The automatic grouping by month was chosen for simplicity and ease of use. This approach reduces user input while still providing a structured way to view and manage goals.  

The user interface also underwent refinements to improve accessibility and user experience. Initially, goal completion was managed using a toggle switch, but this was later changed to a checkbox-style button, which is more intuitive and visually aligns with task completion patterns commonly seen in to-do list apps.  

**Future Enhancements and Conclusion**  
GoalBuddy is a well-structured, easy-to-use app for goal management, but there is room for future enhancements. Features like push notifications for approaching deadlines, progress tracking with graphs, and cloud synchronization could significantly improve the app's functionality. Additionally, allowing users to categorize goals by priority or tag them with custom labels would provide more flexibility.  

In conclusion, GoalBuddy successfully delivers a simple yet effective goal-tracking experience. The combination of SwiftUI and the MVVM (Model-View-ViewModel) architecture ensures a clean and maintainable codebase. The app's design choices prioritize usability and efficiency, making it a practical tool for users looking to stay organized and motivated in achieving their goals.
