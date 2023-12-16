# Live chat application

You can view the app here: http://neilpatel12.pythonanywhere.com/  <br>
## How it works
This Live Chat Application uses Flask for handling HTTP requests, uses SocketIO for real-time communication (no need for data base), and a HTML/CSS for the front end. The server manages chat rooms, user information, nd message history in memory. The real-time communication is done through SocketIO events. This allows for a interactive chat experience!

## Deep Dive into how the Server works using Flask (the micro web framework)
1. Flask Setup: First I initialized the Flask Setup using (‘app’). Then initialize SocketIO instance (‘socketio’) associated with the Flask app. Also, setup a secret key for each session management in Flask.
2. Room Management: I stored information in a HashMap called (rooms = {}), it stored information about the chat rooms, such as number of members and messages. Also, create a (def generate_unique_code(Length):) function to create a new code for each new room.
3. Setting-up Routes: used decorators such as “@app.route("/", methods=["POST", "GET"])” and “@app.route("/room")” to handle events. The (def home():) function handles both GET and POST requests. Renders the home.html template on GET. On POST, processes user input, validates it, and redirects to the appropriate room. The (def room():) function Renders the room.html template, checking if the user is properly authenticated.
4. SocketIO Event Handlers & Notifications: (using Flask/python Decorators)
   - def message(data): Handles incoming messages from clients. Broadcasts the message to all clients in the same room and stores it in the server's memory.
   - def connect(auth): Handles client connections, joins the client to the specified room, and broadcasts a notification about the new user.
   - def disconnect(): Handles client disconnections, updates the number of members in the room, and broadcasts a notification about the user leaving.

## main.py
- Flask Setup: Initializes a Flask app and sets a secret key for session management. <br>
- SocketIO Setup: Initializes a SocketIO instance associated with the Flask app. <br>
- Room Management: Defines a dictionary (rooms) to store information about chat rooms, including the number of members and messages. <br>
- Unique Code Generation: Implements a function (generate_unique_code) to generate a unique code for new chat rooms. <br>
***Routes:*** <br>
- /: Handles both GET and POST requests. On GET, it renders the home.html template. On POST, it processes user input (name, room code) and redirects to the appropriate room with a given code. <br>
- /room: Renders the room.html template, checking if the user is properly authenticated. <br>
***SocketIO Event Handlers:*** <br>
- message: Handles incoming messages from clients, broadcasting the message to all clients in the same room and storing it in the server's memory. <br>
- connect: Handles client connections, joins the client to the specified room, and broadcasts a notification about the new user. <br>
- disconnect: Handles client disconnections, updates the number of members in the room, and broadcasts a notification about the user leaving. <br>
***Server Run:***  <br>
- Runs the Flack app using SocketIO  <br>

## base.html
- Provides the basic structure for HTML templates, including a title, stylesheet link, and a content block.

## home.html
- Uses the base.html by using the {% extends 'base.html' %} statement <br>
- Displays the chat room interface, including the room code, a message box for displaying messages, and an input field for sending messages. <br>
- Utilizes SocketIO to handle real-time communication for message updates. <br>
- Uses JavaScript to dynamically update the message box when new messages are received. <br>
- Uses a for-loop to display existing messages when the page is loaded. <br>

## style.css
- Defines styles for different elements in the application, providing a visually appealing and user-friendly interface.

## When running the program
1. Users access the home page to enter their name and either join an existing room or create a new one. <br>
2. Upon submitting the form, the server processes the information and redirects the user to the corresponding chat room. <br>
3. The chat room page uses SocketIO to establish a real-time connection with the server, enabling instant message updates. <br>
4. Users can send and receive messages in real-time, and the server stores the chat history in memory. <br>
