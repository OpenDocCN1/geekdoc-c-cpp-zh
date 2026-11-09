
## Where to Go from Here

All right, now that all of the administrative stuff is out of the way, it’s time to get started. You can totally do this. Congratulations on taking your first step into the world of coding!

## Part I

### Getting Started with Coding

![](img/5a907eb39993e80f28c82efc2e4632b3_18_0.png)

### In this part . . .

- Understand what code is and what you can build with it.
- Review programming languages used to write code.
- Code for the web using front-end and back-end programming languages.
- Follow the process programmers use to create code.
- Write your first program using code.

## 1 What Is Coding?

### In This Chapter

- Seeing what code is and what it can do
- Touring your first program using code
- Understanding programming languages used to write code

> “A million dollars isn’t cool, you know what’s cool? A billion dollars.”
> 
> —Sean Parker, *The Social Network*

Every week the newspapers report on another technology company that has raised capital or sold for millions of dollars. Sometimes, in the case of companies like Instagram, WhatsApp, and Uber, the amount in the headline is for billions of dollars. These articles may pique your curiosity, and you may want to see how code is used to build the applications that experience these financial outcomes. Alternatively, your interests may lie closer to work. Perhaps you work in an industry in decline, like print media, or in a function that technology is rapidly changing, like marketing. Whether you are thinking about switching to a new career or improving your current career, understanding computer programming or “coding” can help with your professional development. Finally, your interest may be more personal—perhaps you have an idea, a burning desire to create something, a website or an app, to solve a problem you have experienced, and you know reading and writing code is the first step to building your solution. Whatever your motivation, this book will shed light on coding and programmers, and help you think of both not as mysterious and complex but approachable and something you can do yourself.

In this chapter, you will understand what code is, what industries are affected by computer software, the different types of programming languages used to write code, and take a tour of a web app built with code.

### Defining What Code Is

Computer code is not a cryptic activity reserved for geniuses and oracles. In fact, in a few minutes you will be writing some computer code yourself! Most computer code performs a range of tasks in our lives from the mundane to the extraordinary. Code runs our traffic lights and pedestrian signals, the elevators in our buildings, the cell phone towers that transmit our phone signals, and the spaceships headed for outer space. We also interact with code on a more personal level, on our phones and computers, and usually to check email or the weather.

### Following instructions

Computer code is a set of statements, like sentences in English, and each statement directs the computer to perform a single step or instruction. Each of these steps is very precise, and followed to the letter. For example, if you are in a restaurant and ask a waiter to direct you to the restroom, he might say, “head to the back, and try the middle door.” To a computer, these directions are so vague as to be unusable. Instead, if the waiter gave instructions to you as if you were a computer program he might say, “From this table, walk northeast for 40 paces. Then turn right 90 degrees, walk 5 paces, turn left 90 degrees, and walk 5 paces. Open the door directly in front of you, and enter the restroom.” Figure 1-1 shows lines of code from the popular game, Pong. Do not worry about trying to understand what every single line does, or feel intimidated. You will soon be reading and writing your own code.

```javascript
launchPong(function () {
    function colour_sq_random() {
        var num = Math.floor(Math.random() * 4).pow(2, 4);
        return "#" + ("0000" + num.toString(16)).substr(-6);
    }

    pongSettings.ball.size = 15;
    pongSettings.ball.color = colour_sq_random();
    pongSettings.ball.velocity[0] = 5;
    pongSettings.ball.velocity[1] = 5;

});
```

**Figure 1-1:** Computer code from the game Pong.

One rough way to measure a program’s complexity is to count its statements or lines of code. Basic applications like the game Pong have 5,000 lines of code, while more complex applications like Facebook currently have over

### Understanding What Coding Can Do for You

Coding can be used to perform tasks and solve problems that you experience every day. The “everyday” situations in which programs or apps can provide assistance continues to grow at an exponential pace, but this was not always the case. The rise of web applications, internet connectivity, and mobile phones have inserted software programs into daily life, and lowered the barrier for you to become a creator, solving personal and professional problems with code.

### Eating the world with software

In 2011, Marc Andreessen, creator of Netscape Navigator and now venture capitalist, noted that “software is eating the world.” He predicted that software companies would disrupt existing companies at a rapid pace. Traditionally, code powered software used on desktops and laptops. The software had to first be installed, and then you had to supply data to the program. Three trends have dramatically increased the use of code in everyday life:

- **Web-based software:** This software operates in the browser without requiring installation. For example, if you wanted to check your email, you previously had to install an email client either by downloading the software or from a CD-ROM. Sometimes, issues arose when the software was not available for your operating system, or conflicted with your operating system version. Hotmail, a web-based email client, rose to popularity, in part, because it allowed users visiting www.hotmail.com to instantly check their email without worrying about installation or software compatibility. Web applications increased consumer appetite to try more applications, and developers in turn were incentivized to write more applications.
- **Internet broadband connectivity:** Broadband connectivity has increased, providing a fast Internet connection to more people in the last few years than in the previous decade. Today, more than two billion people can access web-based software, up from approximately 50 million only a decade ago.
- **Mobile phones:** Today’s smartphones bring programs with you wherever you go, and help supply data to programs. Many software programs became more useful when accessed on-the-go than when limited to a desktop computer. For instance, use of maps applications greatly increased thanks to mobile phones because users need directions the most when lost, not just when planning a trip at home on the computer. In addition, mobile phones are equipped with sensors that measure and supply data to programs like orientation, acceleration, and current

### *Coding on the job*

Coding can be useful in the workplace as well. Outside the technology sector, coding in the workplace is common for some professions like financial traders, economists, and scientists. However, for most professionals outside the technology sector, coding is just beginning to penetrate the workplace, and gradually starting to increase in relevance. Here are areas where coding is playing a larger role on the job:

![](img/5a907eb39993e80f28c82efc2e4632b3_25_0.png)

- **Advertising:** Spend is shifting from print and TV to digital campaigns, and search engine advertising and optimization relies on keywords to bring visitors to websites. Advertisers who understand code see successful keywords used by competitors, and use that data to create more effective campaigns.

- **Marketing:** When promoting products, personalizing communication is one strategy that often increases results. Marketers who code can query customer databases and create personalized communications that include customer names and products tailored to specific interests.

- **Sales:** The sales process always starts with leads. Salespeople who code retrieve their own leads from web pages and directories, and then sort and qualify those leads.

Retrieving information by copying text on web pages and in directories is referred to as *scraping*.

- **Design:** After creating a web page or a digital design, designers must persuade other designers and eventually developers to actually program their drawings into the product. Designers who code can more easily bring their designs to life, and can more effectively advocate for specific designs by creating working prototypes that others can interact with.

- **Public relations:** Companies constantly measure how customers and the public react to announcements and news. For instance, if a celebrity spokesperson for a company does or says something offensive, should the company dump the celebrity? Public relations people who code query social media networks like Twitter or Facebook, and analyze hundreds of thousands of individual messages to understand market sentiment.

- **Operations:** Additional profit can be generated, in part, by analyzing a company’s costs. Operations people who code write programs to try millions of combinations to optimize packaging methods, loading routines, and delivery routes.
