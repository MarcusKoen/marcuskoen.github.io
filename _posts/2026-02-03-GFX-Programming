---
author: Marcus Koen
title: C++ GFX Programming (SDL2) (In Progress)
---
<style>
html, body {
  margin: 0;
  padding: 0;
  background: #0f0f0f;
  color: #e0e0e0;
  font-family: monospace, system-ui, sans-serif;
}

/* Rain container */
.rain-container {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 1;
  overflow: hidden;
}

/* Individual raindrop */
.raindrop {
  position: absolute;
  width: 1px;
  height: 60px;
  background: linear-gradient(
    to bottom,
    rgba(200, 220, 255, 0),
    rgba(200, 220, 255, 0.35)
  );
  animation: rain linear infinite;
}

/* Falling animation */
@keyframes rain {
  from {
    transform: translateY(-120vh) translateX(0);
  }
  to {
    transform: translateY(120vh) translateX(-80px);
  }
}

/* Variation */
.raindrop:nth-child(1)  { left: 5%;  animation-duration: 0.9s; }
.raindrop:nth-child(2)  { left: 10%; animation-duration: 1.1s; }
.raindrop:nth-child(3)  { left: 15%; animation-duration: 0.8s; }
.raindrop:nth-child(4)  { left: 20%; animation-duration: 1.2s; }
.raindrop:nth-child(5)  { left: 25%; animation-duration: 0.95s; }
.raindrop:nth-child(6)  { left: 30%; animation-duration: 1.05s; }
.raindrop:nth-child(7)  { left: 35%; animation-duration: 0.85s; }
.raindrop:nth-child(8)  { left: 40%; animation-duration: 1.15s; }
.raindrop:nth-child(9)  { left: 45%; animation-duration: 0.9s; }
.raindrop:nth-child(10) { left: 50%; animation-duration: 1.2s; }
.raindrop:nth-child(11) { left: 55%; animation-duration: 0.8s; }
.raindrop:nth-child(12) { left: 60%; animation-duration: 1.1s; }
.raindrop:nth-child(13) { left: 65%; animation-duration: 0.95s; }
.raindrop:nth-child(14) { left: 70%; animation-duration: 1.05s; }
.raindrop:nth-child(15) { left: 75%; animation-duration: 0.85s; }
.raindrop:nth-child(16) { left: 80%; animation-duration: 1.15s; }
.raindrop:nth-child(17) { left: 85%; animation-duration: 0.9s; }
.raindrop:nth-child(18) { left: 90%; animation-duration: 1.2s; }
.raindrop:nth-child(19) { left: 95%; animation-duration: 0.8s; }

  /* Fix code block visibility */
pre, code {
  background-color: #0b0b0b !important;
  color: #f2f2f2 !important;
}

/* Inline code */
code {
  padding: 0.15em 0.35em;
  border-radius: 4px;
}

/* Fenced code blocks */
pre {
  padding: 1em;
  overflow-x: auto;
  border-radius: 6px;
  box-shadow: inset 0 0 0 1px rgba(255,255,255,0.08);
}

/* Optional: monospace consistency */
pre, code {
  font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
}

</style>

<div class="rain-container">
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div>
</div>

# Repository Link
The code for this project can be found [here](https://github.com/MarcusKoen/GFX-Programming-SDL)

# SDL Library Link
The actual library for SDL is found [here](https://www.libsdl.org)

To make the library work with code blocks follow these steps:
1. Get the SDL source code from [github](https://release-assets.githubusercontent.com/github-production-release-asset/330008801/a79538d8-b047-4ed2-bf1c-2229b9190fdd?sp=r&sv=2018-11-09&sr=b&spr=https&se=2026-02-03T11%3A49%3A33Z&rscd=attachment%3B+filename%3DSDL3-3.4.0.zip&rsct=application%2Foctet-stream&skoid=96c2d410-5711-43a1-aedd-ab1947aa7ab0&sktid=398a6654-997b-47e9-b12b-9515b896b4de&skt=2026-02-03T10%3A49%3A09Z&ske=2026-02-03T11%3A49%3A33Z&sks=b&skv=2018-11-09&sig=Kp0ffjOnqYnVcA4mMrf30nWvT8Lshq%2BCNrj5YkB1Ca8%3D&jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmVsZWFzZS1hc3NldHMuZ2l0aHVidXNlcmNvbnRlbnQuY29tIiwia2V5Ijoia2V5MSIsImV4cCI6MTc3MDExODEwNSwibmJmIjoxNzcwMTE2MzA1LCJwYXRoIjoicmVsZWFzZWFzc2V0cHJvZHVjdGlvbi5ibG9iLmNvcmUud2luZG93cy5uZXQifQ.N6me3M-XFpvz1qf9giSzec_drAptY0vOvCt8yKE7UKI&response-content-disposition=attachment%3B%20filename%3DSDL3-3.4.0.zip&response-content-type=application%2Foctet-stream)
2. In the folder is the "include" folder
3. Move the contents of include to C:\Program Files\CodeBlocks\MinGW\include\SDL3
4. In your source code
```
#include <SDL3/SDL.h>
```

No this is all wrong and fucked, this is the steps I used. Note: This is only for Code::Blocks, VC is different.
1. Create a new folder C:/SDL3
2. Download SDL3-devel-3.4.0-mingw.zip. MAKE SURE ITS MINGW
3. Open SDL3-devel-3.4.0-mingw.zip
4. Open x86_64-w64-mingw32
5. Copy include and lib into C:/SDL3
6. Copy bin/SDL3.dll to where your .exe is compiled
7. In Code::Blocks : Project -> Build Options -> Linker Settings -> Other linker options -> Add
-lmingw32
-lSDL3.dll
8. Search Directories
9. Compiler -> C:/SDL3/include
10. Linker -> C:/SDL3/lib
11. Do the same for project build options
12. Change from console to GUI in project build options
13. Test with this
```
#define SDL_MAIN_USE_CALLBACKS 1  /* use the callbacks instead of main() */
#include <SDL3/SDL.h>
#include <SDL3/SDL_main.h>

/* We will use this renderer to draw into this window every frame. */
static SDL_Window *window = NULL;
static SDL_Renderer *renderer = NULL;

#define WINDOW_WIDTH 640
#define WINDOW_HEIGHT 480

/* This function runs once at startup. */
SDL_AppResult SDL_AppInit(void **appstate, int argc, char *argv[])
{
    SDL_SetAppMetadata("Example Renderer Rectangles", "1.0", "com.example.renderer-rectangles");

    if (!SDL_Init(SDL_INIT_VIDEO)) {
        SDL_Log("Couldn't initialize SDL: %s", SDL_GetError());
        return SDL_APP_FAILURE;
    }

    if (!SDL_CreateWindowAndRenderer("examples/renderer/rectangles", WINDOW_WIDTH, WINDOW_HEIGHT, SDL_WINDOW_RESIZABLE, &window, &renderer)) {
        SDL_Log("Couldn't create window/renderer: %s", SDL_GetError());
        return SDL_APP_FAILURE;
    }
    SDL_SetRenderLogicalPresentation(renderer, WINDOW_WIDTH, WINDOW_HEIGHT, SDL_LOGICAL_PRESENTATION_LETTERBOX);

    return SDL_APP_CONTINUE;  /* carry on with the program! */
}

/* This function runs when a new event (mouse input, keypresses, etc) occurs. */
SDL_AppResult SDL_AppEvent(void *appstate, SDL_Event *event)
{
    if (event->type == SDL_EVENT_QUIT) {
        return SDL_APP_SUCCESS;  /* end the program, reporting success to the OS. */
    }
    return SDL_APP_CONTINUE;  /* carry on with the program! */
}

/* This function runs once per frame, and is the heart of the program. */
SDL_AppResult SDL_AppIterate(void *appstate)
{
    SDL_FRect rects[16];
    const Uint64 now = SDL_GetTicks();
    int i;

    /* we'll have the rectangles grow and shrink over a few seconds. */
    const float direction = ((now % 2000) >= 1000) ? 1.0f : -1.0f;
    const float scale = ((float) (((int) (now % 1000)) - 500) / 500.0f) * direction;

    /* as you can see from this, rendering draws over whatever was drawn before it. */
    SDL_SetRenderDrawColor(renderer, 0, 0, 0, SDL_ALPHA_OPAQUE);  /* black, full alpha */
    SDL_RenderClear(renderer);  /* start with a blank canvas. */

    /* Rectangles are comprised of set of X and Y coordinates, plus width and
       height. (0, 0) is the top left of the window, and larger numbers go
       down and to the right. This isn't how geometry works, but this is
       pretty standard in 2D graphics. */

    /* Let's draw a single rectangle (square, really). */
    rects[0].x = rects[0].y = 100;
    rects[0].w = rects[0].h = 100 + (100 * scale);
    SDL_SetRenderDrawColor(renderer, 255, 0, 0, SDL_ALPHA_OPAQUE);  /* red, full alpha */
    SDL_RenderRect(renderer, &rects[0]);

    /* Now let's draw several rectangles with one function call. */
    for (i = 0; i < 3; i++) {
        const float size = (i+1) * 50.0f;
        rects[i].w = rects[i].h = size + (size * scale);
        rects[i].x = (WINDOW_WIDTH - rects[i].w) / 2;  /* center it. */
        rects[i].y = (WINDOW_HEIGHT - rects[i].h) / 2;  /* center it. */
    }
    SDL_SetRenderDrawColor(renderer, 0, 255, 0, SDL_ALPHA_OPAQUE);  /* green, full alpha */
    SDL_RenderRects(renderer, rects, 3);  /* draw three rectangles at once */

    /* those were rectangle _outlines_, really. You can also draw _filled_ rectangles! */
    rects[0].x = 400;
    rects[0].y = 50;
    rects[0].w = 100 + (100 * scale);
    rects[0].h = 50 + (50 * scale);
    SDL_SetRenderDrawColor(renderer, 0, 0, 255, SDL_ALPHA_OPAQUE);  /* blue, full alpha */
    SDL_RenderFillRect(renderer, &rects[0]);

    /* ...and also fill a bunch of rectangles at once... */
    for (i = 0; i < SDL_arraysize(rects); i++) {
        const float w = (float) (WINDOW_WIDTH / SDL_arraysize(rects));
        const float h = i * 8.0f;
        rects[i].x = i * w;
        rects[i].y = WINDOW_HEIGHT - h;
        rects[i].w = w;
        rects[i].h = h;
    }
    SDL_SetRenderDrawColor(renderer, 255, 255, 255, SDL_ALPHA_OPAQUE);  /* white, full alpha */
    SDL_RenderFillRects(renderer, rects, SDL_arraysize(rects));

    SDL_RenderPresent(renderer);  /* put it all on the screen! */

    return SDL_APP_CONTINUE;  /* carry on with the program! */
}

/* This function runs once at shutdown. */
void SDL_AppQuit(void *appstate, SDL_AppResult result)
{
    /* SDL will clean up the window/renderer for us. */
}

```
If this works -> Congrats. If not -> I am sorry
