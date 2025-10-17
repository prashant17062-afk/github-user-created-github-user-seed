GitHub Profile Viewer

Summary
This web application provides a straightforward way to fetch and display public profile information for any GitHub user. By leveraging the GitHub API, it retrieves key details such as the user's name, username, number of public repositories, followers, biography, and the creation date of their account. The application prioritizes user experience by offering real-time status updates for data loading and enhances accessibility through ARIA live regions. It also incorporates a caching mechanism using `localStorage` to remember the last successfully looked-up username.

Setup
To set up and run this application, follow these simple steps:
1.  **Download:** Obtain the `index.html` file.
2.  **Open in Browser:** Open the `index.html` file using any modern web browser (e.g., Chrome, Firefox, Edge, Safari). No web server or additional dependencies are required; it runs directly from the file system.

Usage
1.  **Launch the Application:** Open `index.html` in your web browser.
2.  **Pre-filled Username (if applicable):** If you have previously performed a successful lookup, the username input field will be pre-filled with the last queried username.
3.  **Enter GitHub Username:** In the input box labeled "e.g., octocat", type the GitHub username you wish to inspect (e.g., `github`, `torvalds`).
4.  **Initiate Fetch:** Click the "Fetch Data" button or press the `Enter` key while the input field is active.
5.  **Monitor Status:** The area below the input field, labeled `github-status`, will provide real-time updates:
    *   "Loading data for [username]..." indicates that data is being retrieved.
    *   "Data loaded successfully for [username]." confirms a successful operation.
    *   Error messages (e.g., "GitHub user '[username]' not found.") will be displayed if the lookup fails. These status messages are designed to be accessible to screen readers via `aria-live="polite"`.
6.  **View Profile Details:** Upon a successful fetch, the "User Profile Details" section will populate with the following information:
    *   **Name:** The user's display name.
    *   **Username:** The user's GitHub login.
    *   **Public Repos:** The total count of public repositories.
    *   **Followers:** The number of users following this profile.
    *   **Account Age:** The age of the GitHub account calculated in whole years from its creation date.
    *   **Bio:** The user's public biography.
    *   **Profile URL:** A direct link to the user's GitHub profile page.

Main Code Logic
The core logic of the application is implemented in the JavaScript section embedded within `index.html`.

1.  **DOM Content Loaded:** The script executes only after the entire HTML document has been fully parsed, ensuring all elements are available for manipulation.
2.  **Element References:** Key HTML elements (input field, button, status area, and various `<span>` elements for profile data) are referenced using their respective IDs.
3.  **`localStorage` Caching:**
    *   On page load, the script attempts to retrieve the value associated with the key `lastGithubUser` from the browser's `localStorage`. If a value exists, it is used to pre-fill the username input field, providing convenience for repeat users.
    *   After a successful API call and UI update, the currently queried username is stored back into `localStorage` under the `lastGithubUser` key, ensuring it's available for the next session.
4.  **`fetchGitHubData` Function:**
    *   This `async` function orchestrates the data retrieval process.
    *   **Status Updates:** It first updates the `#github-status` element to inform the user that data is loading and clears any previous profile data. The `aria-live="polite"` attribute on `#github-status` ensures these updates are conveyed to assistive technologies.
    *   **API Request:** It constructs a `fetch` request to the GitHub Users API endpoint (`https://api.github.com/users/{username}`) using the provided username.
    *   **Error Handling:** It robustly checks the `response.ok` property. If `false` (indicating an HTTP error), it throws an error message (e.g., for 404 Not Found) which is then displayed in the `#github-status` area.
    *   **Data Parsing and Display:** Upon a successful response, the JSON data is parsed, and the various `<span>` elements in the "User Profile Details" section are updated with the corresponding information (e.g., `data.name`, `data.public_repos`).
    *   **Account Age Calculation:** The `created_at` field from the API response (an ISO 8601 timestamp) is used to calculate the user's account age in whole years. This is done by comparing the current year with the creation year, with an adjustment made if the current date (month and day) precedes the creation date within the current year to ensure only full years are counted. The result is then displayed in `#github-account-age`.
    *   **Success Confirmation:** Finally, `#github-status` is updated to confirm the successful retrieval of data.
5.  **Event Listeners:**
    *   A `click` event listener is attached to the "Fetch Data" button to trigger the `fetchGitHubData` function.
    *   A `keypress` event listener on the username input field allows users to press `Enter` to initiate the fetch, enhancing usability.

License
This project is open-source and released under the MIT License.

MIT License

Copyright (c) 2023 [Your Name/Organization Here]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

Contact
For any questions, feedback, or issues regarding this application, please reach out to [your_email@example.com].