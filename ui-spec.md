# UI Specification: User Management Screen

## 1. Overview
This document outlines the user interface components, requirements, and behaviors for the User Management screen. The screen is divided into two main sections: a left-hand data grid for listing users and a right-hand form for creating or editing user details.

## 2. Initial State (On Page Load)
* **Data Grid:** Populated with the existing list of users fetched from the database.
* **Top Controls:** * "Hide Disabled User" checkbox should be unchecked by default (unless user preferences dictate otherwise).
* **Details Form (Right Panel):** The form should be in a read-only or disabled state, displaying empty fields until a user is selected from the grid or the "+ New User" button is clicked.

## 3. UI Components & Requirements

### 3.1. Top Action Bar
* **`+ New User` Button:**
  * **Type:** Primary Action Button.
  * **Behavior:** Clicking this button clears all fields in the right-hand form, sets the form title to "New User", enables the input fields, and readies the form for a new entry. Deselects any currently selected row in the data grid.
* **`Hide Disabled User` Checkbox:**
  * **Type:** Toggle control.
  * **Behavior:** When checked, the data grid automatically filters out and hides all rows where the "Enabled" status is `false`. When unchecked, all users are displayed.
* **`Save User` Button:**
  * **Type:** Submit Button (Right-aligned).
  * **Behavior:** Validates the input form. If validation passes, it saves the new user or updates the existing user, refreshes the data grid, and shows a success notification.

### 3.2. Left Panel: User List Grid
* **Structure:** A tabular data grid displaying user records.
* **Columns:**
  * **ID:** Numeric identifier.
  * **User Name:** Alphanumeric text.
  * **Email:** Email address format.
  * **Enabled:** Boolean status (`true` or `false`).
* **Column Features:** Every column header must include **Sort** (Ascending/Descending arrows) and **Filter** (Funnel icon) capabilities.
* **Row Interaction:** Clicking on a row selects it. The selected row must be visually highlighted (e.g., distinct background color). Upon selection, the right-hand form must populate with the selected user's details for editing.

### 3.3. Right Panel: User Details Form
* **Header:** Displays "New User" when creating a record, or "Edit User" when a row is selected from the grid.
* **Fields:**
  * **Username:** Text input. (Required, must be unique).
  * **Display Name:** Text input.
  * **Phone:** Text input (Numeric/Phone format validation).
  * **Email:** Text input (Email format validation required).
  * **User Roles:** Dropdown or Multi-select component. 
    * *Options:* Guest, Admin, SuperAdmin.
    * *Behavior:* Clicking opens a dropdown menu to select one or multiple roles.
  * **Enabled:** Checkbox. 
    * *Default state:* Checked (true) for new users.

## 4. Workflows & Error Handling
* **Validation Errors:** If the user clicks "Save User" while mandatory fields (e.g., Username, Email) are empty or invalid, the system should prevent submission and highlight the specific fields with red borders and appropriate error messages.
* **Unsaved Changes:** If a user modifies the form and attempts to select a different user from the grid without saving, prompt a warning dialog: "You have unsaved changes. Are you sure you want to discard them?"
