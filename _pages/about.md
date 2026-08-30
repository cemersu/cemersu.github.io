---
layout: about
title: about
permalink: /
subtitle: About Me

profile:
  align: right
  image: 1prof_pic.jpg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>METU Mathematics</p>

selected_papers: true # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page

announcements:
  enabled: true # includes a list of news items
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: true
  scrollable: true # adds a vertical scroll bar if there are more than 3 new posts items
  limit: 3 # leave blank to include all the blog posts
---
Welcome to ErsuLabs

Driven by a fundamental curiosity about the mathematical structures and analytical principles that govern complex systems, I created this platform to document and share my academic journey. Here, you will find my research papers, expository lecture notes, technical projects, and writings.

I believe that open exchange and constructive critique are central to academic progress. Please feel free to explore my work and reach out for research discussions, academic feedback, or collaborative opportunities.
<div class="my-3">
  <span id="email-copy-badge" onclick="copyEmail()" class="d-inline-flex align-items-center gap-2 px-3 py-2 border rounded-pill shadow-sm" style="cursor: pointer; user-select: none; transition: all 0.2s ease;">
    <i class="fa-regular fa-envelope text-primary"></i>
    <span class="font-monospace fw-medium">ersulabs@gmail.com</span>
    <i id="copy-icon" class="fa-regular fa-copy text-muted ms-1" style="font-size: 0.85rem;" title="Kopyala"></i>
    <span id="copy-feedback" class="text-success small fw-semibold" style="display: none;">Kopyalandı!</span>
  </span>
</div>

<script>
function copyEmail() {
  const email = "ersulabs@gmail.com";
  navigator.clipboard.writeText(email).then(() => {
    const icon = document.getElementById("copy-icon");
    const feedback = document.getElementById("copy-feedback");
    
    icon.style.display = "none";
    feedback.style.display = "inline";
    
    setTimeout(() => {
      feedback.style.display = "none";
      icon.style.display = "inline";
    }, 2000);
  });
}
</script>

