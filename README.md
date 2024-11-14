# Complyance-Assignment

Here’s a **proper PRD** for the **simplified multi-country support** and **role-based access control** feature, tailored for a 2-3 day timeline:

---

### **PRD: Multi-Country Support and Role-Based Access**

### **Project Overview**:

The goal is to enhance the application with multi-country functionality where users can select a country, and the data they work with is tagged with that country. The country selection should persist across sessions, and role-based access should ensure that Admins have full data management capabilities, while Viewers only have read-only access to data related to their assigned country.

---

### **User Stories & Acceptance Criteria**:

### **1. Country Selection & Persistence** (P0)

- **As a user**, I want to select a country from a dropdown, and it should persist across sessions, so I don’t have to select it again after closing and reopening the app.
- **Acceptance Criteria**:
    - A **country dropdown** should be available in the UI.
    - The selected country is saved in the **user profile**.
    - The selected country **persists** even if the browser tab is closed and reopened.

### **2. Role-Based Access Control** (P0)

- **As an Admin**, I want the ability to create, update, and delete data for the selected country.
- **As a Viewer**, I want to only be able to view data for the country assigned to me.
- **Acceptance Criteria**:
    - **Admins** can perform CRUD (Create, Read, Update, Delete) operations for any data related to the country.
    - **Viewers** can only **view** data related to the country assigned to them.
    - Users' access is determined by their **country** and **role** stored in the user profile.

### **3. Data Creation and Country Tagging** (P0)

- **As a user**, when I create new data, it should automatically be tagged with my selected country.
- **Acceptance Criteria**:
    - Data entries (in tables/forms) must be **tagged** with the selected country when created.
    - The country tag is handled **automatically** in the backend, based on the user’s country profile.
    - The data must be stored in the database with the **country field** associated with it.

---

### **Technical Details:**

### **Frontend**:

1. **Country Dropdown**:
    - A simple **country dropdown** should be implemented in the UI, allowing users to select their country.
    - On country selection, the backend should be updated to save the country in the user’s profile.
2. **Data Creation**:
    - Ensure that any data created through forms or tables is tagged with the user’s country, which is automatically handled in the backend.

### **Backend**:

1. **User Profile**:
    - Add a **`country` field** in the **user profile schema**.
    - This field should be set upon user login or country selection.
    - Example Schema (MongoDB):
    
    ```
    const userSchema = new mongoose.Schema({
      username: String,
      password: String,
      country: String, // Country selected by the user
      role: String, // Admin or Viewer
    });
    
    ```
    
2. **API Endpoints**:
    - **POST /api/user/country**: Endpoint to save the country for the user profile.
    - **GET /api/data**: Endpoint to fetch data filtered by the user’s selected country.
    - **POST /api/data**: Endpoint to create new data tagged with the user’s selected country.
    - **PUT /api/data/:id**: Endpoint to update data and ensure it is tagged with the correct country.
    - **DELETE /api/data/:id**: Endpoint to delete data, ensuring only records matching the user’s country are affected.

---

### **Task Breakdown:**

### **P0 Tasks** (Critical):

1. **Country Selection & Persistence**:
    - Implement the **country dropdown** in the UI.
    - Ensure the country is **saved in the user profile** and persists across sessions (even after the browser is closed and reopened).
2. **Role-Based Access**:
    - Implement basic **role-based access control** where Admins can manage data for any country, and Viewers can only view data for their assigned country.
3. **CRUD Operations with Country Tagging**:
    - Ensure that **new data** created (via forms or tables) is **automatically tagged** with the country based on the user’s profile.
    - Implement the necessary backend logic to handle **CRUD operations** with a country filter.

### **P1 Tasks** (Optional):

- **UI Indicators**:
    - Show the **selected country** (e.g., in the header) to provide feedback to the user on their country choice.
- **Error Handling**:
    - Add basic error handling for the case where **country selection is not set** or **unauthorized access** occurs.

### **P2 Tasks** (Advanced/Optional):

- **Role Management**:
    - Implement functionality for **Admin users** to manage the countries assigned to other users (optional if time permits).

---

### **Acceptance Criteria**:

- **Country Selection**: The country dropdown works, and the selected country persists even after the tab is closed and reopened.
- **Role-Based Access**: Admins can access and manage all data for their country, while Viewers can only view data for their assigned country.
- **Data Creation**: All new data is tagged with the user’s country automatically when created.
- **CRUD Operations**: Data creation, viewing, updating, and deletion are filtered and handled based on the user’s country.

---

### **Testing and Evaluation**:

1. **Test Country Persistence**:
    - Verify that when a user selects a country, it persists after closing and reopening the browser.
2. **Test CRUD Operations**:
    - Verify that newly created data is tagged with the correct country, and CRUD operations are properly filtered by the user’s country.
3. **Test Role-Based Access**:
    - Ensure Admins can access and manipulate data for any country, and Viewers can only view data for their assigned country.