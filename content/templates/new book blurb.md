<%*
// 1. Get all files in the vault 
const files = app.vault.getFiles(); 
// 2. Filter for image files only (jpg, jpeg, png, webp) 
const images = files.filter(f => f.path.startsWith("_assets/covers/") && ["jpg", "jpeg", "png","webp"].includes(f.extension));
// 3. Create a list of filenames for you to pick from 
const imageNames = images.map(f => f.name); 
// 4. Show the suggester (the "autofill" menu) 
const cover = await tp.system.suggester( imageNames, imageNames, false, "Select cover file..." );
if (!cover) return; // Stop if you cancel the menu const 

// 2. This asks for the author
const title = await tp.system.prompt("Book title");
const author = await tp.system.prompt("Author name");
-%>
---
cover: <% cover %>
title: <% title %>
author: <% author %>
tags: book
---

<div class="book-blurb">

![[<% cover %>|150]]

<div class="blurb-text">

**Title:** <% title %> <br>
**Author:** <% author %><br>

(Type your blurb here)

</div>
</div>