# MetaCTF: Antisyphon Flash CTF - Cloud

## Challenge: Breaching Buckets

Initially, I looked at this challenge and thought it might have something to do with steganography due to the use of the photos. However, I spent a little time with the image and couldn't find anything glaringly obvious so I put it down for awhile. I came back and reread the description and thought maybe I could traverse the directories.

First tried just backing off each subdirectory like so:
* https://prod-cdn-user-imgs.s3.us-east-1.amazonaws.com/ksmith3892/2020/03/
* https://prod-cdn-user-imgs.s3.us-east-1.amazonaws.com/ksmith3892/2020/
* https://prod-cdn-user-imgs.s3.us-east-1.amazonaws.com/ksmith3892/

Nothing super exciting by some xml data so then I thought, well maybe we could through in a few .. after each subdirectory
* https://prod-cdn-user-imgs.s3.us-east-1.amazonaws.com/ksmith3892/2020/03/..
* https://prod-cdn-user-imgs.s3.us-east-1.amazonaws.com/ksmith3892/2020/..
* https://prod-cdn-user-imgs.s3.us-east-1.amazonaws.com/ksmith3892/..

And then bingo, that last attempt returned an xml document will all of the photos being hosted on the site. Now, how can I retrieve them using the xml data. Well, I didn't, not yet but I was working (learning) how to parse the xml document.

In the mean time, I just used some bash scripting to pull the images (not the cleanest method) and started browsing them. Yeah, I didn't iterate over the years. I had planned to do that manually.

```
for y in {01..12}; do for x in {01..31}; do curl https://prod-cdn-user-imgs.s3.us-east-1.amazonaws.com/ksmith3892/2019/$y/$x.jpg -o $y$x.png; done; done
```

Started browsing the png's and then, there it was,  
**`https://prod-cdn-user-imgs.s3.us-east-1.amazonaws.com/ksmith3892/2019/09/05.jpg`**  

![0905](https://user-images.githubusercontent.com/55144630/171773258-047b7822-ec16-4088-9075-5ed67af2ecaa.png)

Not the cleanest and most efficient but it got the job done.
