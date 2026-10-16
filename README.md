# Hayder-e
Social app that work to connect the people 
titl:
e name that app Hayder social app

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Hayder Social</title>
<style>
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f0f2f5;
  color: #222;
}
header {
  background: #6941e8;
  color: white;
  padding: 18px;
  text-align: center;
  font-size: 24px;
  font-weight: bold;
}
main {
  max-width: 500px;
  margin: 20px auto;
  padding: 12px;
}
.card {
  background: white;
  border-radius: 14px;
  padding: 16px;
  margin-bottom: 15px;
  box-shadow: 0 2px 8px #00000010;
}
textarea {
  width: 100%;
  min-height: 85px;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 10px;
  font-size: 16px;
  resize: vertical;
}
button {
  background: #6941e8;
  color: white;
  border: 0;
  border-radius: 9px;
  padding: 11px 16px;
  margin-top: 10px;
  cursor: pointer;
}
.post-user { font-weight: bold; }
.post-text {
  white-space: pre-wrap;
  overflow-wrap: anywhere;
  line-height: 1.5;
}
.actions {
  border-top: 1px solid #eee;
  padding-top: 10px;
}
.actions button { margin-right: 8px; }
#message { color: #b42318; font-size: 14px; }
</style>
</head>
<body>
<header>💜 Hayder Social</header>

<main>
  <section class="card">
    <h3>Create a Post ✍️</h3>
    <textarea id="postInput"
      placeholder="What's on your mind?"></textarea>
    <div id="message"></div>
    <button id="postButton">＋ Publish Post</button>
  </section>

  <h3>🏠 Home Feed</h3>
  <section id="feed">
    <article class="card">
      <div class="post-user">👤 Hayder</div>
      <p class="post-text">Welcome to Hayder Social! 🎉
Share your thoughts with everyone.</p>
      <div class="actions">
        <button class="likeButton">♡ Like <span>0</span></button>
        <button class="commentButton">💬 Comment</button>
      </div>
    </article>
  </section>
</main>

<script>
const input = document.getElementById("postInput");
const feed = document.getElementById("feed");
const message = document.getElementById("message");

function connectButtons(card) {
  const like = card.querySelector(".likeButton");
  const comment = card.querySelector(".commentButton");

  like.addEventListener("click", () => {
    const count = like.querySelector("span");
    const liked = like.dataset.liked === "true";
    like.dataset.liked = String(!liked);
    count.textContent = Number(count.textContent) + (liked ? -1 : 1);
    like.firstChild.textContent = liked ? "♡ Like " : "♥ Liked ";
  });

  comment.addEventListener("click", () => {
    const reply = prompt("Write your comment:");
    if (reply && reply.trim()) {
      const p = document.createElement("p");
      p.textContent = "💬 " + reply.trim();
      card.appendChild(p);
    }
  });
}

document.querySelectorAll(".card").forEach(card => {
  if (card.querySelector(".likeButton")) connectButtons(card);
});

document.getElementById("postButton").addEventListener("click", () => {
  const text = input.value.trim();
  if (!text) {
    message.textContent = "Please write something first!";
    return;
  }

  const card = document.createElement("article");
  card.className = "card";

  const user = document.createElement("div");
  user.className = "post-user";
  user.textContent = "👤 Hayder";

  const content = document.createElement("p");
  content.className = "post-text";
  content.textContent = text;

  const actions = document.createElement("div");
  actions.className = "actions";
  actions.innerHTML =
    '<button class="likeButton">♡ Like <span>0</span></button>' +
    '<button class="commentButton">💬 Comment</button>';

  card.append(user, content, actions);
  feed.prepend(card);
  connectButtons(card);

  input.value = "";
  message.textContent = "";
});
</script>
</body>
</html>
