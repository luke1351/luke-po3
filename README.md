# luke-po3   #include <SDL2/SDL.h>
#include <stdbool.h>

int main() {
    SDL_Init(SDL_INIT_VIDEO);
    SDL_Window* window = SDL_CreateWindow("Driving the Pinto",
        SDL_WINDOWPOS_CENTERED, SDL_WINDOWPOS_CENTERED, 800, 600, 0);
    SDL_Renderer* renderer = SDL_CreateRenderer(window, -1, 0);

    SDL_Rect car = { 375, 285, 50, 30 };
    bool running = true;
    SDL_Event event;

    while (running) {
        while (SDL_PollEvent(&event)) {
            if (event.type == SDL_QUIT)
                running = false;
        }

        const Uint8* keystates = SDL_GetKeyboardState(NULL);
        if (keystates[SDL_SCANCODE_LEFT])  car.x -= 5;
        if (keystates[SDL_SCANCODE_RIGHT]) car.x += 5;
        if (keystates[SDL_SCANCODE_UP])    car.y -= 5;
        if (keystates[SDL_SCANCODE_DOWN])  car.y += 5;

        SDL_SetRenderDrawColor(renderer, 0, 0, 0, 255); // Black background
        SDL_RenderClear(renderer);

        SDL_SetRenderDrawColor(renderer, 255, 165, 0, 255); // Orange car
        SDL_RenderFillRect(renderer, &car);

        SDL_RenderPresent(renderer);
    }

    SDL_DestroyRenderer(renderer);
    SDL_DestroyWindow(window);
    SDL_Quit();
    return 0;
}
