---
layout: page
title: About
permalink: /about/
---

<section class="values-section">
  <h2>Our Values</h2>

  <div class="value-item">
    <h3>Inclusive Learning</h3>
    <p>
      EEP supports inclusive learning as an essential component for our facilitator and student experience. EEP aims for all participants, including facilitators, to gain knowledge in engineering, teamwork, and design. EEP recognizes that all students learn differently, and we aim to create an environment that values diversity and enables participation for all students.
    </p>
  </div>

  <div class="value-item">
    <h3>Creativity and Innovation</h3>
    <p>
      To encourage new, unique ways to solve problems and approach situations, EEP is dedicated to encouraging creativity and innovation. This skillset enables students to reach their potential in engineering design challenges.
    </p>
  </div>

  <div class="value-item">
    <h3>Mentorship</h3>
    <p>
      EEP is dedicated to creating meaningful relationships between students, facilitators, and all participants in the program. Through fostering these relationships, confidence and self-empowerment is possible to build in all participants, encouraging the pursuit of engineering and everyday challenges.
    </p>
  </div>
</section>

<div class="page__content">
    <p>See what we are up to on Instagram!</p>
</div>

<div class="insta-card">
    <!-- LightWidget WIDGET --><script src="https://cdn.lightwidget.com/widgets/lightwidget.js"></script>
  <iframe
    src="//lightwidget.com/widgets/ec86b46599bc55da8c145dbaa51ce6aa.html"
    scrolling="no" 
    allowtransparency="true" 
    class="lightwidget-widget">
  </iframe>
</div>

<style>

.values-section {
  max-width: 900px;
  margin: 0 auto;
  padding: 4em 1.5em;
  text-align: left;
}

.values-section h2 {
  text-align: center;
  font-size: 2em;
  font-weight: 700;
  margin-bottom: 1.5em;
  color: #1f2937;
}

.value-item {
  display: grid;
  grid-template-columns: 200px 1fr; 
  gap: 2em;
  align-items: start;
  margin-bottom: 2.5em;
  background: #fff;
  border-radius: 12px;
  padding: 1.5em 2em;
  box-shadow: 0 3px 10px rgba(0,0,0,0.1);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.value-item h3 {
  font-weight: 700;
  font-size: 1.05em;
  color: #1f2937;
  margin: 0;
  text-align: right;
}

.value-item p {
  margin: 0;
  color: #374151;
  line-height: 1.6;
}

@media (max-width: 700px) {
  .value-item {
    grid-template-columns: 1fr;
    text-align: center;
  }

  .value-item h3 {
    text-align: center;
    margin-bottom: 0.5em;
  }
}


.insta-card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 3px 10px rgba(0,0,0,0.1);
  padding: 0.8em;
  max-width: 400px;
  margin: 2em auto;
  overflow: hidden;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.insta-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 6px 15px rgba(0,0,0,0.15);
}

.insta-card .lightwidget-widget {
  width: 100%;
  height: 480px; 
  border: none;
  display: block;
  border-radius: 10px;
}

@media (max-width: 600px) {
  .insta-card {
    max-width: 90%;
  }
  .insta-card .lightwidget-widget {
    height: 400px;
  }
}

.page__content {
  max-width: 900px;
  margin: 0 auto;
  padding: 2em 1em;
  text-align: center;
}

/* Dark Mode looks ugly
@media (prefers-color-scheme: dark) {

  body, .page__content {
    background-color: #121212;
    color: #e5e5e5;
  }

  .insta-card {
    background: #1e1e1e;
    box-shadow: 0 3px 10px rgba(0,0,0,0.6);
  }

  .insta-card:hover {
    box-shadow: 0 6px 15px rgba(0,0,0,0.8);
  }

 
  .insta-card .lightwidget-widget {
    background-color: #1e1e1e;
  }
}
*/
</style>

