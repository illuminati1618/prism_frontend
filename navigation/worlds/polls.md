---
layout: post
title: Worlds
show_reading_time: false
search_exclude: true
permalink: /prism/polls
---

<style>
    body {
        margin: 0;
        font-family: Arial, sans-serif;
        background-color: black;
        color: white;
    }

    .main {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 30px;
    }

    .poll-header {
        background-color: red;
        text-align: center;
        padding: 20px;
        margin-bottom: 20px;
        border-radius: 15px;
        font-size: 24px;
        font-weight: bold;
    }

    .poll-subtitle {
        font-size: 16px;
        color: #ddd;
        margin-top: -10px;
        text-align: center;
    }

    .poll-question {
        color: red;
        font-size: 24px;
        text-align: center;
        margin-bottom: 20px;
    }

    .poll-options {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 60%;
    }

    .poll-option {
        background-color: #666 !important;
        color: white;
        padding: 15px;
        margin: 10px 0;
        border: none;
        text-align: center;
        width: 100%;
        font-size: 18px;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }

    .poll-option:hover {
        background-color: #555 !important;
    }

    .poll-option:active {
        background-color: #333 !important;
    }

    footer {
        margin-top: 20px;
        font-size: 12px;
        color: #aaa;
    }

    /* Form container styles */
    .form-container {
        display: flex;
        flex-direction: column;
        max-width: 800px;
        width: 100%;
        padding: 30px;
        border-radius: 10px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        margin-bottom: 40px;
    }

    .form-container label {
        margin-bottom: 10px;
        font-size: 18px;
    }

    .form-container input,
    .form-container textarea,
    .form-container select {
        margin-bottom: 20px;
        padding: 15px;
        border-radius: 5px;
        border: 1px rgb(95, 95, 95);
        width: 100%;
        background-color: #34495e;
        color: #ecf0f1;
    }

    .form-container button {
        padding: 15px;
        border-radius: 5px;
        border: none;
        background-color: rgb(95, 95, 95);
        color: #ecf0f1;
        cursor: pointer;
        font-size: 18px;
    }

    .form-container button:hover {
        background-color: rgb(95, 95, 95);
    }

    .form-container.group-channel-container {
        background-color: rgb(95, 95, 95);
    }

    .form-container.submit-answer-container {
        background-color: rgb(95, 95, 95);
    }

    /* Table styles for clarity */
    table {
        width: 80%;
        border-collapse: collapse;
        margin-bottom: 30px;
    }
    th, td {
        padding: 10px;
        border-bottom: 1px solid #ccc;
    }
</style>

<script type="module">
    import { pythonURI, fetchOptions } from "{{site.baseurl}}/assets/js/api/config.js";

    async function checkAuthorization() {
        try {
            const response = await fetch(`${pythonURI}/api/id`, fetchOptions);

            if (response.status === 401) {
                window.location.href = "{{site.baseurl}}/login";
            } else if (response.ok) {
                const contentElements = document.querySelectorAll('.content');
                contentElements.forEach(element => {
                    element.style.display = "block";
                });
            }
        } catch (error) {
            console.error("Authorization check failed:", error);
            window.location.href = "{{site.baseurl}}/login";
        }
    }

    checkAuthorization();
</script>

<header class="poll-header">
    Quick Polls
</header>
<p class="poll-subtitle">Your voice, your community</p>

<!-- Original poll form (Form 1) -->
<center>
    <div class="form-container submit-answer-container" id="pollForm1">
        <h2 style="text-align: center;">Submit Your Answer Here</h2>
        <form onsubmit="submitPoll('pollForm1'); return false;">
            <label for="addPollInterests1">What is your favorite genre of music?</label>
            <input type="text" id="addPollInterests1" name="interests" placeholder="Enter your interests" required>
            <button type="submit">Submit</button>
        </form>
    </div>
</center>

<!-- Poll Form 2 -->
<center>
    <div class="form-container submit-answer-container" id="pollForm2" style="display:none;">
        <h2 style="text-align: center;">Poll Question 2</h2>
        <form onsubmit="submitPoll('pollForm2'); return false;">
            <label for="addPollInterests2">What is your favorite movie genre?</label>
            <input type="text" id="addPollInterests2" name="interests" placeholder="Enter your interests" required>
            <button type="submit">Submit</button>
        </form>
    </div>
</center>

<!-- Poll Form 3 -->
<center>
    <div class="form-container submit-answer-container" id="pollForm3" style="display:none;">
        <h2 style="text-align: center;">Poll Question 3</h2>
        <form onsubmit="submitPoll('pollForm3'); return false;">
            <label for="addPollInterests3">What is your favorite book genre?</label>
            <input type="text" id="addPollInterests3" name="interests" placeholder="Enter your interests" required>
            <button type="submit">Submit</button>
        </form>
    </div>
</center>

<!-- Poll Form 4 -->
<center>
    <div class="form-container submit-answer-container" id="pollForm4" style="display:none;">
        <h2 style="text-align: center;">Poll Question 4</h2>
        <form onsubmit="submitPoll('pollForm4'); return false;">
            <label for="addPollInterests4">What is your favorite travel destination?</label>
            <input type="text" id="addPollInterests4" name="interests" placeholder="Enter your interests" required>
            <button type="submit">Submit</button>
        </form>
    </div>
</center>

<script type="module">
    import { pythonURI, fetchOptions } from "{{site.baseurl}}/assets/js/api/config.js";

    window.addPoll = async function addPoll() {

        var user = await fetch(`${pythonURI}/api/user`, fetchOptions);

        const userData = await user.json();
        console.log("User data", userData);

        const username = userData.name;
        // console.log(username)
        const name = `${username}`;
        const interests = document.getElementById('addPollInterests').value;
        const payload = { name, interests };

        try {
            const response = await fetch(`${pythonURI}/api/poll`, {
                ...fetchOptions,
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(payload)
            });
            if (!response.ok) {
                throw new Error('Network response was not ok ' + response.statusText);
            }
            const data = await response.json();
            console.log('Poll created:', data);
            location.reload();
        } catch (error) {
            console.error('Error creating poll:', error);
        }
    }
</script>


<script type="module">
    import { pythonURI, fetchOptions } from "{{site.baseurl}}/assets/js/api/config.js";

    // 1) Inline delete function for a given poll ID
    window.deletePollById = async function(id) {
        const payload = { id };
        try {
            const response = await fetch(`${pythonURI}/api/poll`, {
                ...fetchOptions,
                method: 'DELETE',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(payload)
            });
            if (!response.ok) {
                throw new Error('Network response was not ok ' + response.statusText);
            }
            const data = await response.json();
            console.log(data);
            location.reload();
        } catch (error) {
            console.error('Error deleting poll:', error);
        }
    }

    // 2) For the separate form
    window.deletePollForm = function() {
        const id = document.getElementById('deletePollId').value;
        window.deletePollById(id);
    }

    // 3) Inline update function for a given poll ID
    window.updatePollById = async function(id, newName, newInterests) {
        const payload = { id, name: newName, interests: newInterests };
        try {
            const response = await fetch(`${pythonURI}/api/poll`, {
                ...fetchOptions,
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(payload)
            });
            if (!response.ok) {
                throw new Error('Network response was not ok ' + response.statusText);
            }
            const data = await response.json();
            console.log('Poll updated:', data);
            location.reload();
        } catch (error) {
            console.error('Error updating poll:', error);
        }
    }
</script>

<center>
    <h2>Poll Results</h2>
</center>
<br>

<center>
    <!-- Table with inline editing and inline delete -->
    <table class="submit-answer-container">
        <thead>
            <tr>
                <th>Name</th>
                <th>Result</th>
            </tr>
        </thead>
        <tbody id="poll-data">
            <!-- Rows dynamically added here -->
        </tbody>
    </table>
</center>

<div id="dataOutput"></div>

<script type="module">
    import { pythonURI, fetchOptions } from "{{site.baseurl}}/assets/js/api/config.js";

    // Fetch current user info
    const userResponse = await fetch(`${pythonURI}/api/user`, fetchOptions);
    if (!userResponse.ok) {
        throw new Error('Failed to fetch user info: ' + userResponse.statusText);
    }
    const userData = await userResponse.json();
    const currentUserName = userData.name;  // Used for comparison

    // Fetch poll data and group by name
    try {
        const response = await fetch(`${pythonURI}/api/poll`, fetchOptions);
        if (!response.ok) {
            throw new Error('Network response was not ok ' + response.statusText);
        }
        const data = await response.json();
        console.log('Fetched polls:', data);

        // Group polls by author name
        const groupedPolls = {};
        data.forEach(item => {
            if (!groupedPolls[item.name]) {
                groupedPolls[item.name] = [];
            }
            groupedPolls[item.name].push(item);
        });

        const pollData = document.getElementById('poll-data');
        pollData.innerHTML = '';

        // For each group, create one table row
        Object.entries(groupedPolls).forEach(([name, polls]) => {
            const row = document.createElement('tr');

            // Name cell (author)
            const nameCell = document.createElement('td');
            nameCell.textContent = name;
            row.appendChild(nameCell);

            // Combined poll results cell
            const resultsCell = document.createElement('td');
            polls.forEach(pollItem => {
                const pollContainer = document.createElement('div');
                pollContainer.style.marginBottom = '10px';

                // Input for interests
                const interestsInput = document.createElement('input');
                interestsInput.type = 'text';
                interestsInput.value = pollItem.interests;
                // Disable if not the owner
                if (name !== currentUserName) {
                    interestsInput.disabled = true;
                }
                pollContainer.appendChild(interestsInput);

                // If current user is the owner, add inline update and delete buttons
                if (name === currentUserName) {
                    // Update button
                    const updateButton = document.createElement('button');
                    updateButton.textContent = 'Update';
                    updateButton.style.backgroundColor = 'green';
                    updateButton.style.color = 'white';
                    updateButton.style.border = 'none';
                    updateButton.style.padding = '4px 8px';
                    updateButton.style.marginLeft = '5px';
                    updateButton.style.cursor = 'pointer';
                    updateButton.onclick = function() {
                        window.updatePollById(pollItem.id, name, interestsInput.value);
                    };
                    pollContainer.appendChild(updateButton);

                    // Delete button
                    const deleteButton = document.createElement('button');
                    deleteButton.textContent = 'Delete';
                    deleteButton.style.backgroundColor = 'red';
                    deleteButton.style.color = 'white';
                    deleteButton.style.border = 'none';
                    deleteButton.style.padding = '4px 8px';
                    deleteButton.style.marginLeft = '5px';
                    deleteButton.style.cursor = 'pointer';
                    deleteButton.onclick = function() {
                        window.deletePollById(pollItem.id);
                    };
                    pollContainer.appendChild(deleteButton);
                }
                resultsCell.appendChild(pollContainer);
            });
            row.appendChild(resultsCell);
            pollData.appendChild(row);
        });
    } catch (error) {
        console.error('There has been a problem with your fetch operation:', error);
    }
</script>

<script type="module">
    import { pythonURI, fetchOptions } from "{{site.baseurl}}/assets/js/api/config.js";

    // Array of form IDs in the desired cycling order
    const formIds = ['pollForm1', 'pollForm2', 'pollForm3', 'pollForm4'];

    // On page load, check if a form index was saved previously
    const savedFormIndex = localStorage.getItem('currentFormIndex');
    if (savedFormIndex !== null) {
        const parsedIndex = parseInt(savedFormIndex);
        // Hide all forms at first
        formIds.forEach(id => document.getElementById(id).style.display = 'none');
        // Show the saved form if valid
        if (!isNaN(parsedIndex) && formIds[parsedIndex]) {
            document.getElementById(formIds[parsedIndex]).style.display = 'block';
        } else {
            // Default to first form if index is invalid
            document.getElementById(formIds[0]).style.display = 'block';
        }
    }

    // Submits the poll answer from the given form ID and cycles to the next form
    window.submitPoll = async function(formId) {
        const formDiv = document.getElementById(formId);
        const input = formDiv.querySelector('input[name="interests"]');
        const interests = input.value;

        // Get current user info
        const userResponse = await fetch(`${pythonURI}/api/user`, fetchOptions);
        if (!userResponse.ok) {
            throw new Error('Failed to fetch user info: ' + userResponse.statusText);
        }
        const userData = await userResponse.json();
        const username = userData.name;
        const payload = { name: username, interests: interests };

        try {
            const response = await fetch(`${pythonURI}/api/poll`, {
                ...fetchOptions,
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(payload)
            });
            if (!response.ok) {
                throw new Error('Network response was not ok ' + response.statusText);
            }

            // Once submission succeeds, figure out next form
            const currentIndex = formIds.indexOf(formId);
            const nextIndex = (currentIndex < formIds.length - 1) ? currentIndex + 1 : 0;

            // Save that index in localStorage for the next load
            localStorage.setItem('currentFormIndex', nextIndex);

            // Reload the page (this will cause on-page-load logic to show the next form)
            location.reload();
        } catch (error) {
            console.error('Error creating poll:', error);
        }
    }
</script>