---
layout: post
title: Performance Task 1 Prep
type: issues
courses: {'csp': {'week': 20}}
comments: True
---

# **Holiday Giftinator Performance Task**

## **Purpose of Your Group's Program**
The "Holiday Giftinator" program collects feedback about the website's user experience. The goal is to gather insights from users regarding the website’s design, functionality, and usability, which will be used to improve the overall platform.

## **Purpose of Your Individual Feature(s)**
My individual feature is responsible for implementing the survey functionality on the website. I developed the backend that processes and stores feedback submitted by users, specifically through the `Survey` model and related API endpoints.

---

## **Input/Output Requests**

### **Demo Ways to Input to Your Full Stack Feature**
- **Frontend**: Users submit feedback on the website, including their opinions on design, usability, and other elements. This feedback is sent in a JSON object.
  
- **Backend (API)**: The feedback data is submitted via a POST request, which the backend processes and stores in the database.

### **Using Frontend Show API Request and Present API Response (Live Demo)**
- **API Request Example (Frontend - Survey Submission)**:
```javascript
fetch('http://localhost:8887/api/survey', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    message: 'The website is great, but the navigation could be improved.',
    user_id: 1
  })
})
.then(response => response.json())
.then(data => console.log(data));
```

- **API Response Example**:
```json
{
  "id": 1,
  "message": "The website is great, but the navigation could be improved.",
  "user_id": 1
}
```

### **Using Postman to Show Raw API Request and RESTful Response**
- **Postman Request**:
  - Method: POST
  - URL: `http://localhost:8887/api/survey`
  - Body:
  ```json
  {
    "message": "The website is great, but the navigation could be improved.",
    "user_id": 1
  }
  ```
  
- **Postman Response**:
  ```json
  {
    "id": 1,
    "message": "The website is great, but the navigation could be improved.",
    "user_id": 1
  }
  ```

---

### **Using `db_init`, `db_restore`, `db_backup` to Show Tester Data Creation and Data Recovery**
- **`db_init`**: Initializes the database with sample survey data.
- **`db_restore`**: Restores the database to a previous state with feedback data for testing.
- **`db_backup`**: Creates backups of the feedback data to ensure recovery during testing.

---

## **List Requests**

### **Use of List, Dictionaries, and Database**
- **Lists**: Feedback responses are stored as a list of survey entries in the database, where each entry corresponds to a row.
  
- **Dictionaries**: Each survey entry is represented as a dictionary, with keys like `id`, `message`, and `user_id`, which correspond to columns in the database.

- **Database**: The feedback data is stored in a relational database where each survey is a row, and each attribute (e.g., `message`, `user_id`) is a column.

### **Code Descriptions**
- **Lists (Rows)**: The list of survey responses is mapped to rows in the database.
- **Dictionaries (Columns)**: The dictionary fields correspond to the columns in the database (e.g., `message`, `user_id`).

---

## **Formatting Response Data (JSON) from API into DOM**
- The JSON response returned by the backend is formatted to display success messages and feedback in the DOM. Once the survey data is submitted, the user sees the confirmation message displayed on the webpage.

---

## **Discuss Queries from Database Where You Extract a Python List (Rows)**
- The backend queries the database to retrieve all survey feedback data and returns it as a list of rows, where each row is represented by a Python dictionary.

---

## **Discuss Methods in "Survey" Class to Work with Columns (Create, Read, Delete)**
The backend uses the `Survey` class to handle operations for storing and processing survey feedback.

### **Survey Class Example**:
```python
class Survey(db.Model):
    __tablename__ = 'surveys'

    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    message = db.Column(db.String(255), nullable=False)
    user_id = db.Column(db.Integer, db.ForeignKey('users.id'), nullable=False)

    def __init__(self, message, user_id):
        self.message = message
        self.user_id = user_id

    def __repr__(self):
        return f"Survey(id={self.id}, message={self.message}, user_id={self.user_id})"

    def create(self):
        """Adds a new survey response to the database."""
        try:
            db.session.add(self)
            db.session.commit()
        except IntegrityError:
            db.session.rollback()
            raise IntegrityError("Survey response creation failed due to a database error.")

    def read(self):
        """Returns a dictionary representation of the survey response."""
        return {
            'id': self.id,
            'message': self.message,
            'user_id': self.user_id
        }

    def delete(self):
        """Deletes the survey response from the database."""
        try:
            db.session.delete(self)
            db.session.commit()
        except IntegrityError:
            db.session.rollback()
            raise IntegrityError("Survey response deletion failed due to a database error.")
```

- **Create**: Adds a new survey response to the database.
- **Read**: Returns a dictionary of the survey details.
- **Delete**: Deletes a survey response from the database.

---

## **Algorithmic Code Request**

### **Show the Definition of Code Blocks to Handle a Request**
The backend handles incoming survey feedback via the POST method. Here’s the relevant code block:

```python
@app.route('/api/survey', methods=['POST'])
def add_survey():
    """Endpoint to create a new survey response."""
    try:
        # Get the data from the incoming request
        data = request.get_json()

        # Check if required data is provided
        if 'message' not in data or 'user_id' not in data:
            return jsonify({"error": "Both 'message' and 'user_id' are required."}), 400

        # Check if user exists
        user = User.query.get(data['user_id'])
        if not user:
            return jsonify({"error": "User not found."}), 404

        # Create new Survey instance and save it
        new_survey = Survey(message=data['message'], user_id=data['user_id'])
        new_survey.create()  # Commit to the database

        # Return success response with the newly created survey data
        return jsonify(new_survey.read()), 201

    except Exception as e:
        return jsonify({"error": str(e)}), 500
```

### **Discuss API Class (Code Block) Used to Perform GET, POST, PUT, DELETE Methods**
- **POST Method**: Accepts the feedback data and creates a new survey entry in the database.
```javascript
  try {
      const response = await fetch(`${pythonURI}/api/survey`, {
          ...fetchOptions,
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ message: reviewText })
      });
  } catch (error) {
      console.error("Error submitting feedback:", error);
  }
  ```
- **GET Method**: Not currently implemented, but could be used to retrieve all survey data.
- **PUT Method**: Would be used for updating an existing survey response.
- **DELETE Method**: Deletes a survey response from the database.

---

### **Discuss a Method/Procedure in Class that Contains Sequencing, Selection, and Iteration**
The `add_survey()` method includes:
- **Sequencing**: The steps to validate data, create a new survey, and return the response are executed in order.
- **Selection**: Conditional checks are made to ensure that the required fields (`message`, `user_id`) are present and that the user exists.
```javascript
  let reviewText = document.getElementById("review-text").value;
            if (reviewText.trim() === "") {
                alert("Please enter a review before submitting.");
                return;
            }
            try {
                const response = await fetch(`${pythonURI}/api/survey`, {
                    ...fetchOptions,
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ message: reviewText })
                });
                if (response.ok) {
                    alert("Thank you for your review!");
                    document.getElementById("review-popup").style.display = "none";
                    document.getElementById("review-text").value = "";
                } else {
                    alert("Failed to submit review. Please try again.");
                }
            } catch (error) {
                console.error("Error submitting review:", error);
                alert("An error occurred while submitting the review. Please try again.");
            }
```


- **Iteration**: If needed, iteration could be used to perform operations on multiple surveys, such as retrieving all surveys or deleting multiple surveys at once.
```python
def fetch_chat_history():
    try:
        response = requests.get(f"{BACKEND_URL}/get_chat")
        response.raise_for_status()
        return response.json().get("history", [])
    except Exception as e:
        print(f"Error fetching chat history: {e}")
        return []
```
---

### **Discuss the Parameters (Body of Request) and Return Type (JSONify) of the Function**
- **Parameters**: The `add_survey()` function receives a JSON object containing the `message` and `user_id` fields.
- **Return Type**: The function returns a JSON response with the survey data or an error message.

---

### **Call to Algorithm Request**

### **Show the Definition of Code Block to Make a Request**
The frontend makes a POST request to submit survey data to the backend API using the `fetch` method.

### **Discuss the Call/Request to the Method with Algorithm (Fetch to Endpoint)**
The frontend sends the data via `fetch()` to the `/api/survey` endpoint. This triggers the `add_survey()` method on the backend.

### **Discuss the Return/Response from the Method with Algorithm (Fetch) and How You Handle Data**
The backend responds with a JSON object containing the survey details or an error message. This is handled and displayed on the frontend.
