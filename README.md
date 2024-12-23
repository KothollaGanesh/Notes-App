# Student Notes Management Application

This is a web application that allows users to manage their student notes effectively. The app provides functionality to add, update, delete, and save notes in a table. The notes are also saved locally using `localStorage`, ensuring data persistence across sessions.

## Features
- **Add Notes:** Users can input a note's name and add it to the table.
- **Update Notes:** Existing notes can be updated by clicking the `Update` button.
- **Delete Notes:** Notes can be removed from the table by clicking the `Delete` button.
- **Persistent Data Storage:** Notes are stored in the browser's `localStorage` for retrieval during subsequent visits.

## Technologies Used
- `HTML`: Provides the structure of the application.
- `CSS`: Styles the interface to make it visually appealing.
- `JavaScript`: Implements the interactive functionality and manages local storage.

## Files
- **`index.html`**: Contains the main structure and layout of the application.
- **`style.css`** (inline in the HTML): Defines the appearance of the application.
- **`script.js`** (inline in the HTML): Handles the logic for adding, updating, deleting, and saving notes.

## Installation and Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/student-notes-app.git
   ```
2. Navigate to the project directory:
   ```bash
   cd student-notes-app
   ```
3. Open the `index.html` file in any modern web browser.

## Usage
1. Enter the name of a note in the input field and click `Add to Table` to add it to the list.
2. Use the `Update` button to edit an existing note. The note will be removed from the table and its content will populate the input field for editing.
3. Use the `Delete` button to remove a note from the table.
4. Reload the page to see that your notes persist, thanks to `localStorage`.

## Code Highlights
- **Adding Notes:**
  ```javascript
  function addRow() {
      event.preventDefault();
      const Name = document.getElementById('A').value;
      if (Name === '') {
          alert('Fill the name');
          return;
      }
      const tablebody = document.getElementById('table').querySelector('tbody');
      const newrow = document.createElement('tr');
      newrow.innerHTML = `<td>${Name}</td>
      <td>
          <button class="update" onclick="updaterow(this)">update</button>
          <button class="Delete" onclick="DeleteRow(this)">Delete</button>
      </td>`;
      tablebody.appendChild(newrow);
      document.getElementById('A').value = '';
      saveTabledata();
  }
  ```

- **Persistent Data Storage:**
  ```javascript
  function saveTabledata() {
      const tablebody = document.getElementById('table').querySelector('tbody');
      const rows = Array.from(tablebody.rows);
      const tabledata = rows.map(function(row) {
          return { Name: row.cells[0].innerText };
      });
      localStorage.setItem('tabledata', JSON.stringify(tabledata));
  }

  function loadTableData() {
      const storeddata = localStorage.getItem('tabledata');
      if (!storeddata) return;
      const tabledata = JSON.parse(storeddata);
      const tablebody = document.getElementById('table').querySelector('tbody');
      tabledata.forEach(function(item) {
          const newrow = document.createElement('tr');
          newrow.innerHTML = `<td>${item.Name}</td>
          <td>
           <button class="update" onclick="updaterow(this)">update</button>
           <button class="Delete" onclick="DeleteRow(this)">Delete</button>
          </td>`;
          tablebody.appendChild(newrow);
      });
  }
  ```

## Future Enhancements
- Add search functionality to filter notes.
- Implement sorting options for the table.
- Use a backend server to sync data for cross-device access.

## License
This project is licensed under the `MIT License`.

## Acknowledgments
Special thanks to the developers and educators who inspire us to create and share projects!

