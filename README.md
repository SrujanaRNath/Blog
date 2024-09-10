# Blog
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Blog</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        header {
            background-color: #333;
            color: #fff;
            padding: 10px 0;
            text-align: center;
        }
        header h1 {
            margin: 0;
        }
        .container {
            width: 80%;
            margin: 20px auto;
            background-color: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .post {
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 1px solid #ddd;
        }
        .post-title {
            font-size: 1.8em;
            color: #333;
        }
        .post-content {
            margin: 10px 0;
            line-height: 1.6;
        }
        .write-post {
            margin: 20px 0;
        }
        .write-post textarea {
            width: 100%;
            height: 100px;
            padding: 10px;
            border: 1px solid #ddd;
            margin-bottom: 10px;
        }
        .write-post input[type="text"] {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            margin-bottom: 10px;
        }
        .write-post button {
            background-color: #333;
            color: #fff;
            padding: 10px;
            border: none;
            cursor: pointer;
        }
        footer {
            text-align: center;
            padding: 20px;
            background-color: #333;
            color: #fff;
            position: fixed;
            width: 100%;
            bottom: 0;
        }
    </style>
</head>
<body>

<header>
    <h1>My Blog</h1>
</header>

<div class="container">
    <!-- Display Posts -->
    <div id="posts">
        <!-- Posts will be inserted here dynamically -->
    </div>

    <!-- Write a New Post Section -->
    <div class="write-post">
        <h2>Write a New Post</h2>
        <input type="text" id="postTitle" placeholder="Post Title" />
        <textarea id="postContent" placeholder="Post Content"></textarea>
        <button onclick="savePost()">Submit</button>
    </div>
</div>

<footer>
    <p>&copy; 2024 My Blog. All Rights Reserved.</p>
</footer>

<script>
    // Function to save a new post to localStorage
    function savePost() {
        const title = document.getElementById('postTitle').value;
        const content = document.getElementById('postContent').value;

        if (title && content) {
            const post = {
                title: title,
                content: content,
                timestamp: new Date().toLocaleString()
            };

            let posts = localStorage.getItem('posts');
            posts = posts ? JSON.parse(posts) : [];

            posts.push(post);
            localStorage.setItem('posts', JSON.stringify(posts));

            // Clear input fields after submission
            document.getElementById('postTitle').value = '';
            document.getElementById('postContent').value = '';

            displayPosts(); // Refresh posts list
        } else {
            alert('Please fill out both the title and content.');
        }
    }

    // Function to display all posts from localStorage
    function displayPosts() {
        const postsContainer = document.getElementById('posts');
        postsContainer.innerHTML = '';

        let posts = localStorage.getItem('posts');
        posts = posts ? JSON.parse(posts) : [];

        posts.forEach(post => {
            const postDiv = document.createElement('div');
            postDiv.classList.add('post');
            postDiv.innerHTML = `
                <h2 class="post-title">${post.title}</h2>
                <p class="post-content">${post.content}</p>
                <small>Posted on ${post.timestamp}</small>
            `;
            postsContainer.appendChild(postDiv);
        });
    }

    // Load all posts when the page is loaded
    window.onload = displayPosts;
</script>

</body>
</html>
