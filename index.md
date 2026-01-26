
---
layout: home
title: Home
---
<style>
  body, html {
    margin: 0;
    padding: 0;
    height: 100%;
    background-color: #0f0f0f;       /* Grok-style dark gray – try #111111 or #121212 if you want slightly lighter */
    color: #e0e0e0;
    font-family: monospace, system-ui, sans-serif;
    overflow-x: hidden;
  }

  /* Snow container – covers full viewport */
  .snow-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;           /* lets you click through to content */
    z-index: -1;                    /* behind your markdown content */
    overflow: hidden;
  }

  .snowflake {
    position: absolute;
    width: 8px;
    height: 8px;
    background: #ffffff;
    border-radius: 50%;
    opacity: 0.7;
    box-shadow: 0 0 4px #ffffff;
    animation: snowfall linear infinite;
  }

  @keyframes snowfall {
    0%   { transform: translateY(-100vh) translateX(0); }
    100% { transform: translateY(100vh)  translateX(var(--drift, 0)); }
  }

  /* Generate ~20 snowflakes with random-ish positions, sizes, speeds */
  .snowflake:nth-child(1)  { left: 10%;  animation-duration: 18s; animation-delay: -2s;  width: 6px; height: 6px; }
  .snowflake:nth-child(2)  { left: 25%;  animation-duration: 22s; animation-delay: -5s;  width: 10px; height: 10px; }
  .snowflake:nth-child(3)  { left: 35%;  animation-duration: 15s; animation-delay: -1s;  width: 5px; height: 5px; }
  .snowflake:nth-child(4)  { left: 45%;  animation-duration: 25s; animation-delay: -9s;  width: 9px; height: 9px; }
  .snowflake:nth-child(5)  { left: 55%;  animation-duration: 14s; animation-delay: -4s;  width: 7px; height: 7px; }
  .snowflake:nth-child(6)  { left: 65%;  animation-duration: 20s; animation-delay: -12s; width: 12px; height: 12px; }
  .snowflake:nth-child(7)  { left: 75%;  animation-duration: 16s; animation-delay: -3s;  width: 4px; height: 4px; }
  .snowflake:nth-child(8)  { left: 85%;  animation-duration: 19s; animation-delay: -7s;  width: 8px; height: 8px; }
  .snowflake:nth-child(9)  { left: 15%;  animation-duration: 21s; animation-delay: -10s; width: 11px; height: 11px; }
  .snowflake:nth-child(10) { left: 30%;  animation-duration: 17s; animation-delay: -6s;  width: 6px; height: 6px; }
  .snowflake:nth-child(11) { left: 40%;  animation-duration: 23s; animation-delay: -8s;  width: 9px; height: 9px; }
  .snowflake:nth-child(12) { left: 50%;  animation-duration: 13s; animation-delay: -0s;  width: 5px; height: 5px; }
  .snowflake:nth-child(13) { left: 60%;  animation-duration: 24s; animation-delay: -11s; width: 10px; height: 10px; }
  .snowflake:nth-child(14) { left: 70%;  animation-duration: 18s; animation-delay: -5s;  width: 7px; height: 7px; }
  .snowflake:nth-child(15) { left: 80%;  animation-duration: 20s; animation-delay: -9s;  width: 8px; height: 8px; }
  .snowflake:nth-child(16) { left: 90%;  animation-duration: 16s; animation-delay: -2s;  width: 6px; height: 6px; }
  .snowflake:nth-child(17) { left: 5%;   animation-duration: 19s; animation-delay: -13s; width: 11px; height: 11px; }
  .snowflake:nth-child(18) { left: 20%;  animation-duration: 15s; animation-delay: -4s;  width: 5px; height: 5px; }
  .snowflake:nth-child(19) { left: 95%;  animation-duration: 22s; animation-delay: -7s;  width: 9px; height: 9px; }
  .snowflake:nth-child(20) { left: 12%;  animation-duration: 14s; animation-delay: -1s;  width: 7px; height: 7px; }

  /* Optional: gentle side drift – add to some flakes if you want more realism */
  .snowflake:nth-child(odd)  { --drift: 60px; }
  .snowflake:nth-child(even) { --drift: -50px; }
</style>

<div class="snow-container">
  <div class="snowflake"></div><div class="snowflake"></div><div class="snowflake"></div>
  <div class="snowflake"></div><div class="snowflake"></div><div class="snowflake"></div>
  <div class="snowflake"></div><div class="snowflake"></div><div class="snowflake"></div>
  <div class="snowflake"></div><div class="snowflake"></div><div class="snowflake"></div>
  <div class="snowflake"></div><div class="snowflake"></div><div class="snowflake"></div>
  <div class="snowflake"></div><div class="snowflake"></div><div class="snowflake"></div>
  <!-- That's 18; add more <div class="snowflake"></div> lines if you want denser snow -->
</div>
Welcome. This is a minimal log of things I’m working on or thinking about.
```
⠀⠀⠀⠀⠀⠀⠀⠀⠉⠛⠻⢿⣿⡀⢀⠾⣿⡹⢧⣛⢧⣟⡏⣼⢻⣽⣻⣿⣿⣿⣿⢿⢹⣳⡻⣿⣿⡟⢸⣽⢳⣻⣿⣿⣿⣿⣿⣿⣞⠩⣿⡼⣇⣿⣇⠠⢻⣧⢂⢣⢻⣿⣿⣿⣷⣙⣿⣿⣿⣇
⠀⠀⠀⠀⠀⠀⢀⣾⣷⡄⢢⠠⠈⢀⡾⣛⡿⣝⡳⣏⢿⣽⢠⣟⢻⣷⣿⣿⠿⣛⣯⠏⣳⢷⡻⣽⢞⠅⣻⢸⣏⣷⢻⡼⣏⡿⣏⡿⣽⡂⣽⡃⣯⢟⣻⠀⢃⢿⣎⡆⢏⣿⣿⣿⣿⣿⠹⣿⣿⣿
⠀⠀⠀⠀⠀⠀⣾⡻⣟⡿⠆⠡⢀⡾⡵⣏⡿⣱⢯⡽⣾⡌⣴⣋⣾⣿⠟⣡⢟⡾⠅⢸⣛⡾⣝⣧⡟⢀⡏⢰⣻⡼⢯⡷⣏⡷⣏⡇⣳⠇⣳⡅⢯⣛⡷⠂⠘⡖⢻⡶⡘⣞⣶⢲⣭⣛⠇⢿⣿⣿
⠀⠀⠀⠀⠀⠀⣖⢯⣳⡀⢐⠀⣸⢳⣝⡞⣷⢫⣷⣽⣼⡁⡷⣭⣿⢋⡾⢁⣮⠇⡄⡿⣭⡟⣽⢶⡃⢸⡇⢸⣳⣻⢻⡼⣏⡷⣏⣇⢽⡃⡷⡆⣹⣏⡇⡀⣇⢹⡈⡷⣇⠻⣼⣛⡶⢯⣗⠘⣿⢿
⠀⠀⠀⠀⠀⠀⢠⠀⠄⡁⢈⠀⣯⢻⡼⣹⣷⣯⣾⣿⣿⠁⣇⣿⡿⢸⠃⣸⡞⢰⠸⣝⣧⢿⣹⡞⢱⢸⡅⠸⣧⡟⣯⣗⢯⡽⣝⡞⢸⣁⡷⡇⢼⢧⡃⡇⣿⡄⣷⠸⣳⠈⡷⢯⣽⣛⡎⡀⣿⣫
⠀⠀⠀⠀⠀⠀⠐⢥⡘⢄⠂⢰⣏⢷⡻⣷⣿⢿⣿⣿⣿⠀⡇⡿⡽⡇⢠⢷⡃⡌⣾⡽⢾⣹⢮⡅⡎⢸⠃⡀⣷⣻⢷⣞⡯⣟⡾⡅⢻⢠⢿⡅⡾⢋⢀⡇⡻⣷⢸⡅⢹⡇⢹⣛⡶⣏⡯⠇⣷⣫
⠀⠀⠀⠀⠀⠀⠀⠈⣾⡀⠆⢸⣞⣳⣿⣿⣿⣿⣿⣿⡿⢀⠇⣿⡽⠀⡼⣯⢡⢃⡷⠻⠯⠛⢋⢐⡃⣋⢀⡃⣁⣉⣉⣉⠛⣽⣳⠆⡏⢸⢯⢰⡇⡞⢸⢂⢿⣮⡌⣯⠈⣿⡀⢸⣳⢯⣽⢂⡷⢯
⠀⠀⠀⠀⠀⠀⠀⢰⣟⠻⠀⣻⣿⣿⣿⣿⣿⢺⣿⣟⡟⢠⠘⣷⠏⠀⣿⠃⣋⢨⡶⣶⢯⡟⡈⣼⡇⡟⣼⡇⠀⣿⡿⣽⡇⣿⡽⢰⠃⣾⠇⣾⢰⢣⢸⢘⣓⠋⠃⠿⡀⡸⡇⠆⣿⣿⢾⣸⢼⣻
⠀⠀⠀⠀⠀⠀⠀⠸⢈⣵⡇⣿⣿⣿⡟⠙⠻⣸⢷⡾⣹⠀⠘⣯⠂⢸⣯⠁⡏⢸⡽⣞⡷⢰⢡⣿⢃⠇⣿⣿⠀⣿⣿⣽⠰⣯⡇⡞⢠⡿⢰⠃⡎⣾⠘⣾⣿⣿⣷⢠⠄⣅⠛⠀⢹⣯⣿⢸⣻⢷
⠀⠀⠀⠀⠀⠀⠀⠀⠻⣽⠀⣿⣿⡟⣼⡀⠜⣯⣟⣳⣟⠀⠀⣿⡀⣼⡳⠀⣇⢸⡿⡽⢃⢃⣿⡿⡘⢐⣻⢿⠀⣿⣳⡏⢸⣷⠃⢀⣾⢡⠇⡸⣸⡏⢠⣿⣿⣿⣷⢸⢢⣿⡸⢠⢘⠻⣽⢸⣿⡏
⠀⠀⠀⠀⠀⢀⡒⡀⠀⠉⠄⢹⣿⢰⣟⣇⢂⠰⣯⢷⢯⡀⠄⢟⠀⣷⡇⢲⠹⠘⠁⠁⠀⠀⠉⠁⠁⠹⣻⣿⠀⢹⣿⠇⣾⠇⢀⡾⢡⢪⢆⢳⣿⠃⡾⣛⣛⡿⠿⢸⢸⣿⣇⠃⢸⣿⣮⠈⣷⠇
⠀⠀⠀⠀⠀⢆⡱⠨⢄⠀⠈⠸⣧⠸⣻⢾⡄⠂⢹⣞⣟⡆⠀⢬⠀⠋⠀⠀⠀⠀⢀⠠⠀⡔⠠⠰⣶⣦⣤⣉⠀⡀⣿⢡⡿⢠⡞⠁⣵⠏⣠⣿⠃⣼⠯⠛⠋⠙⠛⠘⠸⠟⣿⠀⢸⣿⢾⢰⣿⢀
⠀⠀⠀⢠⠘⠤⢒⡉⢦⠀⡄⠀⢻⡄⢫⣟⢷⡘⡀⢹⡞⣷⡀⠸⠈⠀⢀⣤⠐⡂⢌⡘⢡⣿⣿⠂⢿⣿⣿⣿⣤⣧⣄⡜⠡⠋⣠⣾⣟⣰⣿⣯⣾⡇⠀⡀⠠⣀⠀⢀⠀⠈⠛⠇⢽⣿⡇⣼⡏⣸
⠀⠀⢀⠆⠘⢬⡁⡈⢠⡇⠐⡆⠈⢳⡄⠻⣎⠳⣌⠀⠙⣍⣁⠀⠀⠀⣾⣷⠠⣵⡀⢘⡀⣼⢣⠇⢸⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠰⠠⢮⡿⢄⢋⡈⣷⣄⠀⠀⠠⣴⢠⡿⢱⣻
⠀⠀⣌⠂⣍⠢⢀⡇⢸⠇⣦⠈⡅⠀⠘⢄⠈⠳⡝⢦⡂⠈⠛⣧⡘⣦⡙⢿⡄⢳⣿⡟⡾⣭⡐⢿⣿⣿⣿⣿⣿⢿⣿⡿⣿⡿⣿⣿⣿⣿⣿⣿⣿⢰⠈⠆⢰⣊⢦⠅⣿⣿⣇⠀⠀⠁⡾⢁⣿⠍
⠀⡔⢢⠁⡆⠁⡼⡆⢸⡃⣽⠀⠆⣴⡶⢀⠁⠀⠈⠳⣍⠂⡀⠀⠑⠈⠿⣷⣿⣦⣨⣭⣥⢴⣶⣿⣿⣿⣿⠅⣽⣿⣿⡿⣿⣟⣯⠿⢿⣽⣿⣿⣿⡈⡷⣖⣿⢞⣍⣰⣿⣿⠇⡠⠂⠔⢠⡾⠋⡰
⠰⡈⠦⠑⣠⢯⣝⡃⢸⡇⢀⡘⠠⣿⢸⢻⠛⡖⡀⠤⡈⠛⠒⠤⡀⠑⣶⣌⣙⠛⣾⣾⢞⡷⡻⣞⣺⢹⣽⣿⣿⢷⣿⡷⢟⣹⣗⡿⣿⣿⣿⣻⣯⣷⣦⢍⡈⢃⢹⣿⣻⢯⣾⠀⠀⠴⠋⠁⡴⠁
⠡⡅⠃⣰⢯⣳⢾⠀⢸⡇⢸⣃⠀⣿⡈⣿⡆⢹⠀⢶⣥⣉⠒⠄⠀⢠⣝⡻⡛⡸⢿⢺⣙⣟⢋⣿⣿⣯⡯⣿⣹⣼⣻⣩⣶⣽⣺⣵⣾⡭⣻⣯⠿⣿⣽⣶⠿⣾⢻⣾⣷⣯⡇⠀⡔⠀⢌⠊⢀⡀
⠱⢀⡃⣽⢺⡵⣫⠀⠊⡅⢰⣻⠀⠘⢷⣬⡳⣈⡁⢸⡾⣝⡿⡆⣮⠈⣷⢟⣰⣛⣗⠾⡼⣪⣴⢔⡨⣶⣷⢽⣾⣿⡽⣯⡾⣜⣿⣾⣿⣧⣭⣚⣋⡻⡿⣯⣾⣿⣯⣿⣿⣷⢀⠓⢀⡜⢬⠇⠸⡄
⠁⠼⢐⡃⠿⣜⠷⠀⢂⠅⣤⡟⣆⢄⠀⠙⢿⣮⣕⠸⣽⣫⢷⢁⣵⠀⣱⣊⣼⢬⣿⢿⣶⣻⣹⣾⣶⣿⣷⣞⣽⣿⣿⢿⡷⠿⣵⠞⣽⣿⢯⣤⣵⡾⣏⣩⣼⣿⣾⡿⢿⡏⣠⢡⣞⡟⡏⠀⣇⠇
⠀⠀⠌⡐⠀⠀⠀⠈⠂⠆⢸⣳⠈⡌⡴⣄⡀⠙⠿⢠⢿⣵⡏⢸⣽⠀⢸⣟⣾⣿⣾⣿⢯⣿⣿⣿⣿⣿⣿⣿⣿⣿⢟⢫⣾⣿⣶⣝⡿⣿⣿⣿⣿⣷⣷⣾⡿⣟⣵⣿⣷⡅⢡⣟⡾⡽⠐⢰⣊⢧
⠀⠀⢣⠀⠀⠀⠀⠀⡁⠄⠘⢽⡆⠰⠀⢻⣳⡄⠀⠘⣿⣞⠇⣟⣾⠁⢸⣿⣿⣿⣿⣿⣷⣿⣿⣿⣿⣿⡿⢟⣯⣾⣿⣿⣿⣿⣿⣿⣿⣶⣔⠙⣿⣿⡿⣫⣾⣿⣿⣿⢿⣿⣦⡙⡾⢡⠃⢦⡙⣮
⠀⠀⢂⠆⠀⠀⠀⠀⢐⠈⠐⡀⠻⣄⠣⠈⢷⣻⡄⠈⣷⡟⢨⣟⣾⠀⡇⠻⣿⣿⣿⣿⣿⣿⡿⢫⣵⣶⣿⣿⣿⣿⣿⣿⢏⣽⣛⠿⣿⣿⡿⠼⣿⠏⣾⣿⣿⢋⡋⠘⣿⢿⣿⣿⣦⡙⢰⢢⡝⣳
⢀⠀⠀⠂⠀⡀⠀⠀⢈⠜⡀⠐⠄⡈⠂⡡⠀⢻⣽⠀⣿⠇⣼⣟⡾⠈⣇⢸⣮⡛⢿⣿⠟⣡⣾⣿⣿⣿⣿⣿⣿⠿⣫⣿⣿⣿⣿⣷⡘⢿⡀⠀⠁⢀⣾⢟⡵⠋⠀⡇⢈⠻⠯⣿⡿⣻⣦⣬⣘⠳
⠀⠈⠀⠀⠀⠀⠀⠀⢀⠊⡔⠈⠰⠠⠁⠄⠁⠀⠹⡀⣿⢀⣿⣿⣽⠃⣯⠀⢿⡿⢃⣴⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣭⡻⢿⣿⣿⣿⣿⣮⣑⣀⣤⣭⡷⠋⠀⠀⢰⢁⡾⣷⠀⣩⣾⣿⣿⣿⣿⣿
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠌⠀⠀⠀⠐⠠⠈⡐⠀⠀⠀⡏⣼⣿⣿⣯⡇⣿⠄⣠⣴⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣍⣻⢿⣿⣿⣿⡿⠟⠁⠀⠀⠀⠀⠼⣸⡽⡞⣰⣿⣿⣿⣿⡿⣿⣿
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠡⡁⢄⡈⠐⠀⠃⣿⣿⣿⡿⢃⣡⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣍⠛⠿⢿⣿⣿⣿⣿⣷⣝⠛⠁⠀⠀⠀⠀⠀⠀⠀⡇⣟⢎⣼⣿⣿⣿⠟⠉⣴⣿⣿
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⡁⠂⠐⠡⠂⢠⣿⠟⣫⣴⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣦⣀⠈⠛⢿⣿⣿⣿⣿⣦⡀⠀⠀⠀⠀⠈⠀⡿⢣⣾⣿⣿⠟⢡⢎⣾⣿⣿⣿
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⡐⡀⠀⠀⠀⠘⣡⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣯⣟⡿⣿⣿⣿⣿⣿⣿⣦⡀⠈⠻⢿⣿⣿⣿⣆⡀⠀⠀⠀⠀⢃⣿⣿⡿⠁⠀⢠⣿⣿⣿⣿⣿
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢄⠡⡁⢆⢀⣿⣿⣿⡿⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣶⣽⡻⢿⣿⣿⠟⠀⠀⠀⠀⠙⠻⣿⣿⣿⣄⠀⠀⢠⡿⣿⠞⣽⡅⠀⢜⡿⡿⣻⣿⣿
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠐⠢⠁⠀⠘⡉⢉⠀⡀⠀⠙⠛⠿⠿⠿⠛⠿⠋⠉⠛⠛⠻⢿⣿⣿⡿⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠻⣿⡟⠁⠀⠁⢈⠏⣶⢹⠆⠀⠀⠉⠀⠹⢿⡿
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢡⠐⡈⠰⢀⠂⠄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠉⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠙⠂⠀⢀⣪⣶⡹⡎⡇⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠠⢂⠁⠆⢡⠈⢂⠡⢂⠐⡀⠆⡐⠀⠀⠀⠀⠐⠀⢀⠀⠀⠀⠀⠀⠄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢿⣿⣿⡕⡀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠐⢂⠉⡐⢂⠡⠌⡐⢂⠡⠐⠂⡔⠀⢠⠀⠄⡀⢂⠀⠀⠀⠀⠄⠂⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⢷⣿⣿⣆⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠐⡈⠤⢁⠂⠆⢂⡁⠆⣈⠡⠡⣀⠃⠀⢧⠐⠁⠀⡀⠆⡐⠠⢀⠀⡀⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠻⣿⣿⣷
```
⣄⠀⠀⠀⠀⠀
```
