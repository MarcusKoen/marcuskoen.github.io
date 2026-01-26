---
layout: home
title: Home
---

<style>
html, body {
  margin: 0;
  padding: 0;
  background: #0f0f0f;
  color: #e0e0e0;
  font-family: monospace;
}

.snow-container {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 1;
}

.snowflake {
  position: absolute;
  width: 6px;
  height: 6px;
  background: white;
  border-radius: 50%;
  opacity: 0.7;
  animation: snowfall linear infinite;
}

@keyframes snowfall {
  from { transform: translateY(-10vh); }
  to   { transform: translateY(110vh); }
}

.snowflake:nth-child(1) { left: 10%; animation-duration: 12s; }
.snowflake:nth-child(2) { left: 30%; animation-duration: 16s; }
.snowflake:nth-child(3) { left: 50%; animation-duration: 14s; }
.snowflake:nth-child(4) { left: 70%; animation-duration: 18s; }
.snowflake:nth-child(5) { left: 90%; animation-duration: 15s; }
</style>

<div class="snow-container">
  <div class="snowflake"></div>
  <div class="snowflake"></div>
  <div class="snowflake"></div>
  <div class="snowflake"></div>
  <div class="snowflake"></div>
</div>

Welcome. This is a minimal log of things I’m working on or thinking about.
