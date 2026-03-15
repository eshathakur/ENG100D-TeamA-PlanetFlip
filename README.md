# Reef Rescuer Game
Reef Rescuer is an educational game suited for ages 11-14 focused on coral reefs and the impacts different pollutants (plastic trash, oil spills, and algae) have on ocean life. It is coded on the platform Construct 3. This project was developed for [PlanetFlip](https://planetflip.org/), a non profit organization that works with UC San Diego to combat climate change.

# Tutorial for using Github with Construct: 
[GitHub and Construct](https://www.construct.net/en/tutorials/collaborate-construct-2390)

# How to Test on Different Devices: 
1. Open project on Construct
2. Go to menu -> project -> remote preview
3. You should see a QR code, a link, and an option to select the starting screen
4. Use the QR code or link to open on the device you’re testing

# Guide to Editing, Adding, & Removing Trivia Questions & Answers
Every question is grouped inside a "Level" category ("level_1", "level_2", "level_3"). Inside these levels, each individual question is formatted as a block enclosed in curly brackets { } containing three pieces of information:
1. "question": The text the player will read.
2. "answers": A list of four possible choices inside square brackets [ ].
3. "correct_index": The number that tells the game which answer is right. Note: We start counting at 0 so, 0 = A, 1 = B, 2 = C, and 3 = D.

**To edit an existing question:**
1. Open quiz_data.json.
2. Locate the level and the specific question block you want to change.
3. To change the question text: Edit the text inside the quotation marks next to "question".
4. To change the answers: Edit the text inside the quotation marks for any of the four options in the "answers" list.
5. To change which answer is correct: Change the number next to "correct_index" to 0, 1, 2, or 3. Example: If you want to change the correct answer for the first question in Level 1 from "C" to "A", you would change "correct_index": 2 to "correct_index": 0.

**How to Add a New Question:**
Note: The logic is currently hardcoded to ask exactly 3 questions per level (it checks if CurrentQuestion equals 4 to end the level). To add a 4th question, you would also need to update that number in EventTrivia so the game knows to ask it
1. Go to the level where you want to add the question (e.g., "level_1").
2. Scroll to the very last closing curly bracket } of that level's questions.
3. Add a comma , directly after that last bracket.
4. Paste a fresh question block right below it. Should look like this:

~~~
    }, 
    {
      "question": "Your new question here?",
      "answers": \["A. Option one", "B. Option two", "C. Option three", "D. Option four"\],
      "correct_index": 0
    }
  ],
~~~

**How to Remove a Question:**
1. Locate the block of code for the question you want to delete.
2. Delete everything from its opening curly bracket { to its closing curly bracket }.
3. Check the commas: In JSON files, items in a list are separated by commas, but the last item in a list must not have a comma after it. If you deleted the last question in a level, make sure the new "last" question doesn't have a lingering comma at the end


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

# Global Variables
**TotalScore (Number, initial 0):** Calculates the final score by adding the gameplay level score to the quiz score.

**SummaryData (String, initial ""):** Tracks the current level's trivia questions and the player's specific answers so they can be displayed on the end-screen.

**Unlocked_level (Number, initial 1):** Keeps track of the highest level the player has permanently unlocked.

**CurrentLevel (Number, initial 0):** Tracks the specific level the player is currently playing so the game loads the correct trivia and thresholds.

**CurrentQuestion (Number, initial 1):** Tracks which of the 3 trivia questions the player is currently answering.

**quizScore (Number, initial 0):** Keeps track of the points the player earned or lost exclusively during the quiz.

**Correct (Number, initial 0):** Stores the index (0-3) of the correct answer for the current trivia question.

**SelectedColorBoxUID (Number, initial -1):** Represents the individual color box (out of the 8) the user has selected (touched/clicked)

**DiverColor (String, initial “black”):** Stores the player’s chosen color for their diving suit

**LevelScore (Number, initial 0):** Keeps track of the player's point earned during the level

**StageStartTime (Number, initial 0):** Tracks the time when level begins

**StageDuration, 2, 3 (Number, initial 60, 80, 100):** Stores how many seconds the level lasts

**maxBarWidth (Number, initial 400):** Stores the width of the progress bar

**scrollSpeed, 2, 3 (Number, initial 100, 75, 60):** Stores the scrolling speed of background.

**Non_paused(Boolean, initial true):** Set to true while the game is played(not paused).

# Possible Future Features
**Fish Index:**
* We have the designs on our Figma for this: [Figma](https://www.figma.com/design/ww14HqBcso0oVjvqOgkg77/ENG-100D?node-id=509-70&t=xUEWmldVYaD6SP91-1)
* After each level is completed there is a Post Level Summary page that shows the score to the user and it has two button options: Help Today or Next Level. We did not have time with the scope given but we would've added an i/information icon button in the top right corner of that page that would open/minimize a pop up page which would be a Fish Index.
* The Fish Index would showcase the different fish the user saw in each level, they could tap on each fish icon which would have its fish species listed underneath, and a little pop up page would come up that would share more relevant information about the fish, and it would have an x button in the top right corner to minimize that pop up.
* There are also right and left scroll arrows on the sides of the fish index so the user can see all the different types, in our prototype only 5 fish were seen on each page.

**Sound Effects/Background music:**
* We did not have time with the allotted scope but we would’ve liked to add sound effects throughout the game, such as: sound effects for each button pressed, background music during each level/entire game, sound effects for each trash/algae/oil spill collected, and sound effects for each fish/healthy coral hit

**Game finish summary page:**
* We currently do not have this but it would be great to have an overall game finished summary page when all levels have been passed

**Visual point indicator during each level:**
* We also did not have time for this in the scope, we would have liked to add visual icons such as +10 in green font, or -10 in red font when collecting trash/algae/oil spill or hitting fish/healthy coral.
