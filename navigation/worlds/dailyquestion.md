---
layout: post 
search_exclude: true
show_reading_time: false
permalink: /prism/dailyquestion
---

<!-- Link to Custom CSS and Script -->
<link rel="stylesheet" href="{{site.baseurl}}/navigation/worlds/style.css">
<script src="{{site.baseurl}}/navigation/worlds/script.js" defer></script>

<header class="heading">
    <h1>Daily Question</h1>
    <p>Engage with today's topic!</p>
</header>

<div class="container">
    <!-- Dynamic Question Header -->
    <h2 id="dynamic-question">Choose a topic to begin.</h2>

    <!-- Quiz and Free Response Containers -->
    <div id="quiz-container" style="display: none;"></div>
    <div id="free-response-container" style="display: none;"></div>

    <!-- Dropdown Menu for Topics -->
    <div class="dropdown">
        <button>Pick a Topic</button>
        <div class="dropdown-content">
            <a href="#" class="topic-link">Technology</a>
            <a href="#" class="topic-link">Health</a>
            <a href="#" class="topic-link">Environment</a>
            <a href="#" class="topic-link">Education</a>
        </div>
    </div>
</div>

<footer class="copyright">
    <p>© 2023 Prism. All rights reserved.</p>
</footer>
