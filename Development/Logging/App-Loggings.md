# App Content Loggings

Apps log data using the Json notation. The following table describes the logged data with examples on how the data is saved. In addition data is annotated on when they are logged. 

## Logged Data

| App/Module   |      Data      |  Example |
|----------|---------------| -------------|
| ABC | <ul><li>Selected game mode (robot uses spelling board) <sup>(1)</sup></li><li>Drafted letter from A-Z <sup>(1)</sup></li></ul> | ``` "useLetterSpellingBoard":false, ``` <br> ``` "letter":"G" ``` |
| Communication | <ul><li>Count of characters; -1 on error <sup>(1)</sup></li></ul> | ``` "data": "613" ``` |
| Macarena | <ul><li>If app start with music and motion was successful <sup>(1)</sup></li></ul> | ``` "startSuccessful":"true" ``` |
| Workout | <ul><li>Single motion excercise started <sup>(1)</sup></li><li>Name of launched workout <sup>(1)</sup></li><li>Name of finished workout <sup>(2)</sup></li><li>Music turned on/off <sup>(1,3)</sup></li></ul> | ``` "exerciseName":"Kopf_bewegen_Intro","action":"playExercise" ``` <br> ``` "volume":true ``` |
| Content Player: <ul><li>Jukebox</li><li>Meditation</li><li>Poems</li><li>Storytelling</li></ul>| <ul><li>File name of media <sup>(1)</sup></li><li>Media volume <sup>(1,3)</sup></li><li>Animation mode <sup>(1,3)</sup><ul><li>full body</li><li>torso</li><li>off</li></ul></li></ul> | ``` "file":".../repo/Jukebox/Liebe/Mama - Heintje.ogg" ``` <br> ``` "animation":"torso" ``` <br> ``` "volume":7 ``` |
| Content Player Quiz: <ul><li>Audio</li><li>Character</li><li>Hints</li><li>Keywords</li><li>Proverb</li><li>Quiz</li></ul> | <ul><li>Content started <sup>(1)</sup></li><li>Content finished <sup>(2)</sup></li></ul> | ``` "file":"Tiere" ``` |

1: Logged on content start; 2: Logged on content end; 3: Logged on content change