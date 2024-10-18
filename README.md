#include <SFML/Graphics.hpp>
#include <SFML/Audio.hpp>
#include <iostream>
#include <vector>
#include <cstdlib>

int main() {
    // Create the main game window
    sf::RenderWindow window(sf::VideoMode(800, 600), "Matatu Racing - Nairobi Streets");
    
    // Load textures (matatu, obstacles, passengers)
    sf::Texture matatuTexture, obstacleTexture, passengerTexture;
    if (!matatuTexture.loadFromFile("images/matatu.png") || 
        !obstacleTexture.loadFromFile("images/obstacle.png") || 
        !passengerTexture.loadFromFile("images/passenger.png")) {
        std::cout << "Error loading images!" << std::endl;
        return -1;
    }

    // Create sprites for matatu, obstacles, and passengers
    sf::Sprite matatuSprite(matatuTexture);
    matatuSprite.setPosition(375, 500);  // Initial position for matatu

    // Set initial variables
    float matatuSpeed = 5.0f;
    int score = 0;
    std::vector<sf::Sprite> obstacles;
    std::vector<sf::Sprite> passengers;

    // Load background music tracks (ensure they're in OGG format for SFML)
    sf::Music music;
    std::vector<std::string> playlist = {"music/track1.ogg", "music/track2.ogg", "music/track3.ogg"};
    size_t currentTrack = 0;
    if (!music.openFromFile(playlist[currentTrack])) {
        std::cout << "Error loading music!" << std::endl;
        return -1;
    }
    music.setVolume(50);  // Set volume to 50%
    music.play();  // Play the first track

    // Game loop
    while (window.isOpen()) {
        sf::Event event;
        while (window.pollEvent(event))
