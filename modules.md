---
layout: page
title: Modules
permalink: /modules/
---

<div class="page__content">
    <p>Click any card below to view the full Google Slides presentation.</p>
  
  <!-- Jump Button -->
  <button class="jump-button" onclick="document.getElementById('curriculum').scrollIntoView({ behavior: 'smooth' });">
  Jump to Curriculum
  </button>

  <div id="slides-gallery" class="grid grid--p-3"></div>

  <div id="error-message" style="display:none; margin-top:2em; color:#a33;">
    <strong>Error Loading Slides</strong>
    <p id="error-details" style="margin-top:.5em;"></p>
  </div>
</div>

<script>
/* ====================================================================
   Replace this URL with your published Google Sheet CSV link.
   File → Share → Publish to web → “Comma-separated values (.csv)”
   ==================================================================== */
const GOOGLE_SHEET_CSV_URL = "https://docs.google.com/spreadsheets/d/e/2PACX-1vS3Ie5LEkZ29Fr0FsHN1T2i57rCozJNG84gtmUBKHpPp8-EE4zJj-i6IaJYOC8f3t64egWCD9LqDDJG/pub?gid=0&single=true&output=csv";


const gallery = document.getElementById("slides-gallery");
const errorBox = document.getElementById("error-message");
const errorDetails = document.getElementById("error-details");

function getFileIdFromUrl(url) {
  const match = url.match(/\/d\/([a-zA-Z0-9_-]+)/);
  return match ? match[1] : null;
}

function generateSlideUrls(fileId) {
  const embed = `https://docs.google.com/presentation/d/${fileId}/embed?start=false&loop=false`;
  const thumb = `https://drive.google.com/thumbnail?id=${fileId}&sz=w480`;
  return {embed, thumb };
}


function parseCsv(text) {
  const rows = text.trim().split("\n");
  if (rows.length < 2) return [];
  return rows.slice(1).map(line => {
    const cols = line.split(/,(?=(?:(?:[^"]*"){2})*[^"]*$)/).map(c => c.replace(/^"|"$/g,"").trim());
    const rawUrl = cols[0], title = cols[1] || "Untitled";
    const fileId = getFileIdFromUrl(rawUrl);
    if (!fileId) return null;
    const { viewUrl, embed, thumb } = generateSlideUrls(fileId);
    return { title, embed, thumb };
  }).filter(Boolean);
}


function createSlideCard(slide) {
  const card = document.createElement("div");
  card.className = "card slide-card";
  card.innerHTML = `
    <div class="card__image">
      <a href="${slide.embed}" target="_blank" rel="noopener">
        <img src="${slide.thumb}" alt="Thumbnail for ${slide.title}"
             onerror="this.src='https://placehold.co/480x270/e5e7eb/6b7280?text=No+Thumbnail'">
      </a>
    </div>
    <div class="card__content" style="text-align:center;">
      <p><strong>${slide.title}</strong></p>
    </div>`;
  return card;
}


async function loadSlides() {
  if (GOOGLE_SHEET_CSV_URL === "YOUR_CSV_EXPORT_URL_HERE") {
    errorDetails.textContent = "Please set the GOOGLE_SHEET_CSV_URL in the script.";
    errorBox.style.display = "block";
    return;
  }

  try {
    const res = await fetch(GOOGLE_SHEET_CSV_URL);
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    const csv = await res.text();
    const slides = parseCsv(csv);

    if (!slides.length) {
      gallery.innerHTML = "<p>No slides found in the published sheet.</p>";
      return;
    }

    slides.forEach(slide => gallery.appendChild(createSlideCard(slide)));
  } catch (err) {
    console.error(err);
    errorDetails.textContent = err.message;
    errorBox.style.display = "block";
  }
}

document.addEventListener("DOMContentLoaded", loadSlides);
</script>

<section id="curriculum" class="curriculum-section">
  <h2>The Curriculum</h2>

  <div class="curriculum-intro">
    <p>
      Our curriculum is currently designed for half a school year, one college semester. It typically spans 5–7 weeks, but can be modified to fit each school’s calendar. Each week, we facilitate a sixty-minute module which provides an introduction to engineering, the design process, and its importance in society.
    </p>
  </div>

  <div class="curriculum-topics">
    <h3>Topics Covered</h3>
    <ul>
      <li>
        <strong>Introduction to Engineering</strong>
        <ul>
          <li>Importance of collaboration and communication</li>
          <li>Create community guidelines to follow during group work</li>
        </ul>
      </li>
      <li>
        <strong>Engineering Around You</strong>
        <ul>
          <li>Introduce the different types of engineering and discuss specific responsibilities of each</li>
          <li>Discuss and identify where engineering can be found in the world around us</li>
        </ul>
      </li>
      <li>
        <strong>Customer Discovery</strong>
        <ul>
          <li>Learn the importance of needs assessment through "customer interviews"</li>
          <li>Identify and write a problem statement based on customer needs</li>
        </ul>
      </li>
      <li>
        <strong>Engineering Design Process</strong>
        <ul>
          <li>Learn the key steps in the Engineering Design Process</li>
          <li>Apply the Engineering Design Process through a team design challenge</li>
        </ul>
      </li>
      <li>
        <strong>Sharing Your Design</strong>
        <ul>
          <li>Practice developing and presenting materials</li>
          <li>Learn what "peer review" means and practice by doing a feedback session</li>
        </ul>
      </li>
    </ul>
  </div>
</section>

<style>

.page__content {
  max-width: 900px;
  margin: 0 auto;
  padding: 2em 1em;
  text-align: center;
}

#slides-gallery {
  margin-top: 2em; 
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5em;
  justify-items: center;
}

.slide-card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 3px 10px rgba(0,0,0,0.1);
  padding: 0.8em;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.slide-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 6px 15px rgba(0,0,0,0.15);
}

.slide-card img {
  width: 100%;
  height: auto;
  border-radius: 10px;
  margin-bottom: 0.8em;
}

.slide-card .card__content p {
  margin: 0;
  font-weight: 600;
  color: #333;
}

#error-message {
  margin-top: 3em;
  padding: 1em;
  background: #ffe6e6;
  border: 1px solid #ffcccc;
  border-radius: 8px;
}

/*
@media (prefers-color-scheme: dark) {

  body, .page__content {
    background-color: #121212;
    color: #e5e5e5;
  }

  .slide-card{
    background: #1e1e1e;
    box-shadow: 0 3px 10px rgba(0,0,0,0.6);
  }

  .slide-card:hover {
    box-shadow: 0 6px 15px rgba(0,0,0,0.8);
  }

  .slide-card .card__content p {
    color: #f1f1f1;
  }

  #error-message {
    background: #3b1e1e;
    border: 1px solid #7a3b3b;
    color: #ffbaba;
  }
}
*/

.curriculum-section {
  max-width: 900px;
  margin: 0 auto;
  padding: 3em 1.5em;
  color: #374151;
}

.curriculum-section h2 {
  text-align: center;
  font-size: 2em;
  font-weight: 700;
  margin-bottom: 1.5em;
  color: #1f2937;
}

.curriculum-intro p {
  line-height: 1.6;
  margin-bottom: 2em;
  text-align: left;
  max-width: 750px;
  margin-left: auto;
  margin-right: auto;

}

.curriculum-intro p{
  background: #fff;
  border-radius: 12px;
  padding: 1.5em 2em;
  box-shadow: 0 3px 10px rgba(0,0,0,0.1);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.curriculum-topics h3 {
  text-align: center;
  font-size: 1.5em;
  font-weight: 700;
  margin-bottom: 1.5em;
  color: #1f2937;
}

.curriculum-topics > ul {
  list-style: none;
  padding: 0;
  margin: 0 auto;
  max-width: 800px;
}

.curriculum-topics > ul > li {
  margin-bottom: 2.5em;
  text-align: center;
}

.curriculum-topics strong {
  display: block;
  font-size: 1.2em;
  font-weight: 700;
  color: #111827;
  margin-bottom: 1em;
}

.curriculum-topics ul ul {
  list-style-type: disc;
  text-align: left;
  padding-left: 2em;
  margin: 0 auto;
  max-width: 650px;
}

.curriculum-topics ul ul {
  background: #fff;
  border-radius: 12px;
  padding: 1.5em 2em;
  box-shadow: 0 3px 10px rgba(0,0,0,0.1);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.curriculum-topics li li {
  margin-bottom: 0.6em;
  line-height: 1.5;
  color: #374151;
}


@media (max-width: 700px) {
  .curriculum-section {
    padding: 2em 1em;
  }
  .curriculum-topics strong {
    font-size: 1.1em;
  }
  .curriculum-topics ul ul {
    padding-left: 1.2em;
  }
}

</style>



