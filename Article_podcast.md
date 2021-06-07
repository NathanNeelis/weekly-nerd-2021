## No sound and still enjoying a podcast

Ever needed a different solution for a podcast because you were not able to listen to the audio? Probably not right? Well, during the minor Web Design & Development I met Darice and she lost her ability to hear sound. In other words, she is deaf. My assignment was to create a fitting solution for her to enjoy podcasts. Currently, she sometimes has to wait weeks on the transcriptions, which, in a lot of cases, consist of just a lot of text without any podcast feeling to it. These texts often read worse than a normal article because nobody thought about readability and styling. But how do you let someone still experience the podcast feeling when you have no audio? Well, it involves exclusive design, a lot of testing and a bit of creativity. In this article you will read about my process to find a solution exclusively designed for Darice.  
  
[Link to Darice her personal website](https://www.darice.org/)    
  
### Exclusive design
Exclusive design is designing for the needs of a specific person. This person may or may not have a disability to consider. In making an exclusive design I took a close look at the person I was designing for. In my case, Darice. Before we started, we got to know each other a bit. Unfortunately, we had to do this online because of the Covid-19 pandemic but I learned that she is actually an accessibility expert and a front-end developer. Because of this I added some font styling functionality to my final concept I might otherwise not have. Back to exclusive design, as I mentioned these designs are made for a specific person.This means that this design may not work for other people with the same disability. However, it may turn out that it does work if you test it in your own specific case. Now that I’ve mentioned testing, I might as well start explaining how I got the best result in my design.

### Getting the best result
Testing, testing and testing some more. But what are we testing? Normally I would start with a design, probably start testing my concept as soon as possible and iterate on the design along the way. Now you might think, but that’s how it should be right? You start testing in an early stage so you can change the direction of your solution. Yes, this is true, and this is how I learned it during my study but for exclusive design I took a slightly different approach which worked very well. So instead of testing my concept and iterating on it, I was testing different solutions.   
  
During my first test I assumed that instead of listening to a podcast, Darice probably had to read them. Based on this assumption, I wanted to test which preferences she had for reading texts online regarding the font, font size and line-height. So I build some sliders and checkboxes that changed the look of a part of an random podcast transcription. The Funny thing was, that when Darice tested this, she preferred having the controls. She told me her preferences but also that these preferences might change during the day, for example, she might like a bigger font size and line-height later in the evening then she would like during the day.  
  
For my second test, I wanted to try to re-create the podcast feeling (more than) instead of having just a wall of text. I experimented with dialogs appearing over time, while a bubble with the speaker’s name was bouncing as if he was speaking/typing. I also tested this concept with user input instead of over time, so Darice had to click on the speaker bubbles to let the next dialog show up, but this was not something she would see herself using. The over time test however was a success. The timings were not really on point but the idea was very well thought of.   
  
For the third and last test, I wanted to test how I could add nuances to the podcasts because in text, you cannot hear if someone is being sarcastic, surprised, or angry. You can also not read when there is an (awkward) silence for example. So, I did some test where I added gifs for expressions, like being surprised. For Darice I tried to use gifs from the tv-show Friends because she likes that tv-show a lot. It Turned out that Darice is a fan of gifs even if they’re not specifically from Friends. I also tested a small iteration on the second test because I had a good idea, but I didn’t know if she would like it or not. She commented that my speaker bubbles would be annoying in the long run. This got me trying to think of a better and since I was testing with a podcast from a lecturer of mine, I thought it might be funny to create speaking avatars. She liked this idea but on the condition I got them animated as if they were speaking. I didn’t include that in my test due to the time I had to create it.  
  
During this course I wasn’t the only one testing with Darice for a fitting solution and another student called Stan tested a feature that highlighted the spoken word at that moment in the podcast. So instead of my tests that showed a whole dialog, he highlighted the already spoken words and the word currently being spoken in a different color. This way you can read with the actual podcast speed. Darice liked this a lot and I decided I preferred this way over my test of showing whole dialogs over time.  
  
### Reading a podcast
In the end, I gathered all my test results and added all successfully tested components together in one final concept. In this concept, you can start playing the podcast which would then highlight the word that is being spoken at that time and also highlight the already spoken words with a different color. This really gives the feeling of a podcast while you might not even hear the audio. I also added the font preferences options and I added nuances and some funny animations. To finish my concept, I added avatars that where animated as if speaking while there was being spoken by someone in the podcast. I animated the eyes and mouths of both avatars and after following a lip sync tutorial, I actually succeeded in letting the avatars speaking somewhat realistic.  


### But how does it work under the hood?
Since this wasn’t a very technical course, we were free to fake it. In this prototype, I added data manually to the code, but there are options to do this automatically. The most important data here are time stamps. Each word has a timestamp that is being revered to the timestamp of the playing audio file of the podcast. I added these timestamps manually, but there are software options for getting these timestamps. 

#### Spans
Each word from the transcript is in a span. This span has a few different classes and an ID that contains information about that word. An example of a span with one word is the following:
```HTML
<span class="words vasilis neutral" id="ts11.000">Yeah, </span>
```
The span breaks down into three data items: speaker, lip sync state and timestamp.

#### Speaker
The first class with data is ‘vasilis’ this is the speaker of that word. My podcast has only two speakers, so this value changes between two datapoints. Either Vasilis or Espen. 

#### Lip sync
The second class with data is ‘neutral’ this is one of the seven lip sync mouths. You can also have classes like ‘aei’, ‘thl’, ‘qw’, ‘smile’ etc.. All of these classes represent the shape the mouth makes when the word is spoken. Smile is not a lip sync mouth but just a smile, you could see it as the default state. 
  
![mouth phonemes](https://user-images.githubusercontent.com/55492381/116434004-50b4bb00-a84a-11eb-9516-4c39908e2a2e.png)  
  
#### Timestamps
The last data point in the span is the name of the ID. It always contains ‘ts’ plus a number. TS stands for TimeStamp and the number behind it is the time in the podcast when the word is spoken. In the javascript, I refer the timestamp in the ID with the current timestamp of the audio and so highlights the words.

```JAVASCRIPT
let spns = document.querySelectorAll('.box span')
let audi = document.getElementById("adi");

const highlight = "rgb(252, 186, 3)"
const highlightO = "rgba(252, 186, 3, 0.3)"

    for (i = 0; i < spns.length; i++) {
        var time = Number(spns[i].id.slice(2));
        if (time < audi.currentTime) {
            if (i > 0) spns[i - 1].style.backgroundColor = highlightO;
            spns[i].style.backgroundColor = highlight;
        }
    }
```

### Looking back
During this project, I experienced how important working with other students is. Although we all had our own progress and design solution, we learned from each other’s tests. In the end, we each created a fitting solution for Darice. She confirmed this by writing a blog about our podcast experimentation, and I quote;  
  
> “Their willingness to think outside the box and come up with accessible solutions is in stark contrast with companies/developers/content makers that see accessibility as a last-minute addition." 
  
She showcased some of our solutions and I must admit, it made me proud. All this progress in just three weeks, imagine what we could do given more time and resources!   


### Looking to the future
I always thought accessibility was something for the visually impaired and how these people needed access to your website. But there is more, a lot more. I experienced this firsthand with Darice, but this is just one individual with her specific limitations. Everyone has limitations and preferences and we, as designers, can find fitting solutions for everyone, if we just start talking about the user’s needs and test our concept thoroughly. This course gave me a unique experience in the future I would like to strive for more accessible design. Although primarily used for individual persons the exclusive design approach can also be a very good start in finding a solution fit for a much larger group.  


