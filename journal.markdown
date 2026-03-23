---
layout: page
title: Journal
permalink: /journal/
---

## [1.0](#)

# A real journal might serve you better. Nonetheless feel free to use this space to write your journal entries.

#### This tool creates a dated journal entry you can copy for your own records or notes.

<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Journal App</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div class="journal-container">
      <form id="journal-form">
        <textarea style="resize: vertical; width: 500px;"
          id="journal-input"
          class="journal-entry"
          placeholder="I am grateful for ..."
          required
        ></textarea>
        <br>
        <textarea style="resize: vertical; width: 500px;"
          class="journal-entry"
          placeholder="What's on your mind?"
          required
        ></textarea>
        <br>
        <textarea style="resize: vertical; width: 500px;"
          class="journal-entry"
          placeholder="I feel ... "
          required
        ></textarea>
        <br>
          <button type="submit" class="journal-submit" style="padding: 12px 24px; background-color:rgb(116, 116, 116); color: white; border: none; border-radius: 6px; font-size: 16px; cursor: pointer; transition: background 0.2s;">Enter</button>
              </form>
              <div id="entries-list"></div>
            </div>
            <script>
              const form = document.getElementById("journal-form");
              const textareas = form.querySelectorAll(".journal-entry");
              const entriesList = document.getElementById("entries-list");
              function formatDate(date) {
          return date.toLocaleDateString(undefined, {
            year: "numeric",
            month: "long",
            day: "numeric",
          });
              }
              function getEntryText(texts, date) {
          return (
            `${formatDate(date)}\n` +
            `${texts[0]}\n\n` +
            `${texts[1]}\n\n` +
            `${texts[2]}`
          );
              }
              function addEntry(texts, date) {
          const entryDiv = document.createElement("div");
          entryDiv.className = "journal-entry-block";
          entryDiv.innerHTML = `
              <h3>Your Journal Entry</h3>
              <p class="journal-date">${formatDate(date)}</p>
              <div class="journal-entry">
                <p>${texts[0].replace(/\n/g, "<br>")}</p>
                <p>${texts[1].replace(/\n/g, "<br>")}</p>
                <p>${texts[2].replace(/\n/g, "<br>")}</p>
              </div>
              <button class="copy-entry-btn" type="button">Copy Entry</button>
            `;
          entriesList.prepend(entryDiv);
     // Add copy functionality
        const copyBtn = entryDiv.querySelector(".copy-entry-btn");
        copyBtn.addEventListener("click", function () {
          const entryText = getEntryText(texts, date);
          navigator.clipboard.writeText(entryText).then(() => {
            copyBtn.textContent = "Copied!";
            setTimeout(() => (copyBtn.textContent = "Copy Entry"), 1500);
          });
        });
      }
      form.addEventListener("submit", function (e) {
        e.preventDefault();
        const values = Array.from(textareas).map((t) => t.value.trim());
        if (values.every((v) => v)) {
          addEntry(values, new Date());
          textareas.forEach((t) => (t.value = ""));
        }
      });
    </script>
<br>
<h4>Check out our <a href="/2025/06/17/guide-to-journalling.html">post</a> on journalling for more tips!</h4>
  </body>
</html>
