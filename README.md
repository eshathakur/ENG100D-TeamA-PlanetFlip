# ENG100D-TeamA-PlanetFlip
# Tutorial for using Github with Construct: 
[GitHub and Construct](https://www.construct.net/en/tutorials/collaborate-construct-2390)

# How to Test on Different Devices: 
1. Open project on Construct
2. Go to menu -> project -> remote preview
3. You should see a QR code, a link, and an option to select the starting screen
4. Use the QR code or link to open on the device you’re testing

# Guide to Editing, Adding, & Removing Trivia Questions & Answers

# Context & Event Sheets
**StartPage & EventStartPage:** The title screen of the game. It has two buttons: Help Today which takes the user to a page with more information on how to help coral reefs, and Start which takes the player to the start of the game story. 

**Level1 & EventLevel1:** The game page for level 1. Stage duration is 60 seconds. The target score is 100 points. When this layout is loaded, it changes the diver’s swimsuit to the color the user chooses. Every 1\~3 seconds, the fish is created and its picture is set to random one out of four different images. When the fish hits the diver, it is destroyed and subtracts the score by 5. A trash is created every second and its picture is set to random one out of seventeen different images. When the trash hits the diver, it is destroyed and adds the score by 7. Corals are created every 1.5\~3 seconds and its picture is set to random one out of thirty-six different images. When the coral hits the diver, it degrades the image and subtracts the score by 10. When a diver is clicked during the game it moves down, otherwise floats up. When the diver goes out of the screen, it pushes back inwards so that the diver stays on the screen. The progress bar fills in 60 seconds, and after time is up, it goes to the trivia page. 
There is a pause button at the top right of the screen. If it is pressed, it pauses the game and shows the pause menu with four buttons: resume, restart, help, and home. Resume button closes the pause menu, Restart button restarts the stage of the current level, Help button takes the user to the learn more page, and Home button takes the user to level select page.

**Level2 & EventLevel2:** The game page for level 2. The basic system is the same as level 1, but some variables are set to different values. Stage duration is 80 seconds. The target score is 150 points. Fish image is randomly chosen from three options in level 2. When they hit the diver, it changes the color instead of destroying. Trash images are also randomly chosen from ten algae pictures. There is slightly less trash than level 1 because they are created every 1.2 seconds.

**Level3 & EventLevel3:** The game page for level 3. The basic system is the same as previous levels, but some variables are set to different values. Stage duration is 100 seconds. The target score is 200 points. Fish image is randomly chosen from three options in level 3. When they hit the diver, it changes the color if it is an octopus, otherwise it changes its picture to nothing (looks like it is destroyed). Trash images are also randomly chosen from oil spill pictures. There is slightly less trash than level 2 because they are created every 1.4 seconds.

**DiverCustomization & EventDiverCustomization:** This screen allows the player to choose the color of their diver’s suit. The player has 8 options to choose from: black, pink, red, orange, gray, blue, purple, and green. Afterwards, the player is then taken to the tutorial.

**Tutorial & EventTutorial:** Handles and displays both generic and level specific tutorials. It changes text, container sizes, positions, and visibility depending on level selection. Before entering any level, the tutorial explains how to play the game. Level 1’s tutorial has information on trash, Level 2 has information on algae, and Level 3 has information on oil spills. All levels also include the time limit and the point threshold to pass.

**LearnMorePage & EventLearnMorePage:** Handles outside educational links and gives a few tips on how the player can take action to help coral reefs in the real world. It opens web pages about coral reef protection and quizzes when links are tapped.

**LevelEnd & EventLevelEnd:** Calculates the player's total score and displays the end-of-level results. It contains specific pass/fail score thresholds for Level 1 (100 points), Level 2 (150 points), and Level 3 (200 points). Passing unlocks the next level and plays victory animations (like saving clownfish, sea turtles, or octopuses), while failing asks the user to try again.

**LevelSelectPage & EventLevelSelectPage:** Controls which levels a player can access based on their progression. At the beginning of the layout, the game checks the progress and set the buttons’ frame and opacity. Unlocked levels are shown at 100% opacity with its fish pictures. Otherwise, the opacity is set to 99% with a lock picture on the button. Clicking an available level updates the current level tracker and sends the player to the Tutorial layout for that corresponding level.

**StoryStart & EventStoryStart:** Initiates the game's opening story. It uses a typewriter effect to display a welcome message from King Triton about saving the Great Barrier Reef. A timer runs for 4 seconds, after which a next button appears, allowing the player to go to the diver customization screen.

**Trivia & EventTrivia:** Manages the quiz mechanics by fetching a quiz_data.json file via AJAX. It loads questions and multiple choice answers, and dynamically shrinks the text font from 18pt to 14pt if the answer string is wider or taller than the answer box. When an answer is tapped, it awards +10 points for correct answers and subtracts -10 points for incorrect ones, logs the result in a summary string using color-coded text, and loads the next question.
