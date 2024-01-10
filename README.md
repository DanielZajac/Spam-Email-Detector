# Spam Detector - Assignment 1
> Course: CSCI 2020U: Software Systems Development and Integration


## Project Information
Have you ever tried to check your email only to see an inbox full of spam? Maybe you've looked for an important email 
you were supposed to receive, only to find out it was incorrectly placed in your spam folder? For this assignment, we 
created a program that detects spam emails using a naive Bayes' algorithm on a set of sample spam and 'ham' emails.
The more emails you add into the 'train' folder, the better the final results will be. This program was built fully in 
IntelliJ IDEA, by Daniel Zajac, David Garcia and Heisn Nithysingha.

> Here is a screenshot of our application displaying the results of our spam detection process:
![dashboard.png](dashboard.png)

### Project Improvements
While implementing the naive Bayes' theorem, we made a few key observations. Firstly, words that were extremely common 
in both files did not need to be filtered out, since they have little effect on our algorithm when calculating the 
probability a file is spam. We also noticed that in our algorithm, words that only showed up in one category during 
training, would produce non-meaningful results for the probability a file is spam, such as NaN or negative infinity, 
since we use natural logarithms to balance out the probabilities. To avoid this issue, we revalued these probabilities 
(which were previously 1 and 0), to 0.99999998 and 0.11 respectively (Note that values closer to 0 or 1 sway our algorithm more). The
first probability is extremely close to 1 because if we encounter a word that has only ever been in spam files, then it 
is unlikely ham files will suddenly start using this word, so we want to give these words a large weight in deciding the 
probability that a file is spam. On the other hand, if we encounter a word that we have only ever seen in ham files, 
then there is still a chance that spam files will try to use these words in the future so that they are not detected as 
easily by spam detectors such as ours. Due to this reasoning, we use a probability of 0.11 which sways our decision less 
(but still a decent amount), so that these words do not 'overpower' our algorithm. When looking at the threshold used to 
make the final decision between spam and ham, we realized that this is a surface level change, and should be left to the 
user of this program to decide how strict the decision should be. We think that 50 (in a range from 0 to 100) is a good 
threshold, however changing this does not affect the algorithm, so it can be changed at any point if you value a 
different accuracy or precision.

We also included an 'About us' page, which has clickable links with our GitHub profiles attached. 

### How to run
To run this project, you must first install IntelliJ IDEA, GlassFish 7.0.0 (or similar versions) and git. 
- First, navigate to our GitHub repository at
https://github.com/DanielZajac/Spam-Email-Detector. Select the 'code' 
dropdown menu, and copy the HTTPS link under the 'clone' tab.
- Then, open any shell of your choice, and navigate to your desired directory, where you will clone the project.
- type 'git clone *link*', where *link* represents the HTTPS link you copied from our repository. 
- Now, open the clone repository in IntelliJ. You wil see a pop-up in the bottom right about a maven build script, 
where you click the load button.
- To run the local server, you must first configure glassfish. To do this, click 'Edit Configurations' in the top right 
of IntelliJ, then click 'Add Configuration' and select GlassFish local. In the menu that pops up, type domain1 into the 
domain entry box, then switch to the 'Deployment' tab and select 'spamDetector:war exploded'.
- At this point, you can click the green arrow near the top right to run the local server.
- When the server loads, navigate to the 'SpamDetectorClient' folder and open the 'index.html' file.
- In this file, the UI in the top right will display buttons with your downloaded browsers' icons. Click on whichever 
browser you prefer, which will open the webpage and display the results of our spam detector.

### External Resources

Jackson was used as an external dependency aside from the default Jakarta dependencies.
The ObjectMapper class from Jackson was used to create JSON strings to be sent in Response objects to the client.
The code for these dependencies can be copied from the 'pom.xml' file.

[1] https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind

[2] https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-annotations

