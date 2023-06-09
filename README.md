# GUESS WHO
Main Links: [[Github]](https://github.com/ArnauDIMAI/CLIP-GuessWho) [[App]](https://share.streamlit.io/arnaudimai/clip-guesswho/main/app_qesq.py)

Related Links: [[CLIP]](https://openai.com/blog/clip/) [[Celeba]](https://mmlab.ie.cuhk.edu.hk/projects/CelebA.html)

The aim of the game, as in the original one, is to find a specific image from a group of different images of a person's face. To discover the image, the player must ask questions that can be answered with a binary response, such as "Yes and No". After every question made by the player, the images that don't share the same answer that the winning one are discarded automatically. The answer to the player's questions, and thus, the process of discarding the images will be established by CLIP. When all the images but one have been discarded, the game is over.


The "Guess Who?" game has a handicap when it uses real images, because it is necessary to always ensure that the same criteria are applied when the images are discarded. The original game uses images with characters that present simple and limited features like a short set of different types of hair colors, what makes it very easy to answer true or false when a user asks for a specific hair color. However, with real images it is possible to doubt about if a person is blond haired or brown haired, for example, and it is necessary to apply a method which ensures that the winning image is not discarded by mistake. To solve this problem, CLIP is used  to discard the images that do not coincide with the winner image after each prompt. In this way, when the user asks a question, CLIP is used to classify the images in two groups: the set of images that continue because they have the same prediction than the winning image, and the discarded set that has the opposite prediction. The next figure shows the screen that is prompted after calling CLIP on each image in the game board, where the discarded images are highlighted in red and the others in green.
![CLIP](paper_result_man.png)


## Select Images
The first step of the game is to select the images to play. The player can press a button to randomly change the used images, which are taken from the CelebA data set. This data set contains 202,599 face images of the size 178×218 from 10,177 celebrities, each annotated with 40 binary labels indicating facial attributes like hair color, gender and age. (see next figure).
![CLIP](paper_images.png)


## Ask Questions
The game will allow the player to ask the questions in 4 different ways:

### 1. Default Question
This option consist on select a question from a list. A drop-down list allows the player to select the question to be asked from a group of pre-set questions, taken from the set of binary labels of the Celeba data set. Under the hood, each question is translated into a pair of  textual prompts for the CLIP model to allow for the binary classification based on that question. When they are passed to CLIP along with an image, the model responds by giving a greater value to the prompt that is most related to the image. (see next figure).
![CLIP](paper_question.png)

### 2. Write your own prompt
This option is used to allow the player introducing a textual prompt for CLIP with his/her own words. The player text will be then confronted with the neutral prompt, "A picture of a person", and the pair of prompts will be passed to CLIP as in the previous case. (see next figure)
![CLIP](paper_1query.png)

### 3. Write your own two prompts
In this case two text input are used to allow the player write two sentences. The player must use two opposite sentences, that is, with an opposite meaning. (see next figure).
![CLIP](paper_2query.png)

### 4. Select a winner 
This option does not use the CLIP model to make decisions, the player can simply choose one of the images as the winner and if the player hits the winning image, the game is over. (see next figure).
![CLIP](paper_winner.png)


## Punctuation
To motivate the players in finding the winning image with the minimum number of questions, a scoring system is established so that it  begins with a certain number of points (100 in the example), and decreases with each asked question. The score is decreased by subtracting the number of remaining images after each question. Furthermore, there are two extra penalties. The first is applied when the player uses the option "Select a winner". This penalty depends on the number of remaining images, so that the fewer images are left, the bigger will be the penalty. Finally, the score is also decreased by two extra points if, after the player makes a question, no image can be discarded.


## Acknowledgements
This work has been supported by the company Dimai S.L and next research projects: FightDIS (PID2020-117263GB-100), IBERIFIER (2020-EU-IA-0252:29374659), and the CIVIC project (BBVA Foundation Grants For Scientific Research Teams SARS-CoV-2 and COVID-19).

