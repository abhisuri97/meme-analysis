# Meme analysis 

Just run the ipynb. To generate the scrape, open chrome console on your favorite page and run the following until your chrome runs out of memory (or whenever you'd like to stop gathering posts).

DETAILED STEPS

0. Paste the JS snippet at the bottom of this readme into your chrome console. This will start scrolling  your page.
1. Type in `clearInterval(intervalID)` to stop scrolling (when you have seen enough posts).
2. Then call `copy(JSON.stringify(getPostAttrs()))`)
3. Lastly, create a file called `posts.json` and paste in your data. Then put the file into the same directory as the ipynb and run :)

```js
var scrollToBottom = function() {
    console.log('scrolled!');
  window.scrollTo(0, document.body.scrollHeight);
}
var delay = 2000;
var intervalID = setInterval(scrollToBottom, delay);

function getPostAttrs() { 
	return Array.from(document.getElementsByClassName('_4-u2 mbm _4mrt _5jmm _5pat _5v3q _7cqq _4-u8')).map(i => {
    var obj = { 
        timestamp: Array.from(i.getElementsByClassName('_5ptz'))[0] ? Array.from(i.getElementsByClassName('_5ptz'))[0].getAttribute('data-utime') : 0,
        authorName: Array.from(i.getElementsByClassName('fwb'))[0] ? Array.from(i.getElementsByClassName('fwb'))[0].textContent : '',
        id: Array.from(i.getElementsByClassName('_5pcq'))[0] ? Array.from(i.getElementsByClassName('_5pcq'))[0].getAttribute('href').split('/')[4] : undefined,
        likes: Array.from(i.getElementsByClassName('_3dlh _3dli'))[0] ? Array.from(i.getElementsByClassName('_3dlh _3dli'))[0].textContent.match(/\d+([^\s]+)/g) : ["0"]
    }
    if (obj.likes == null) { obj.likes = "9" } else { obj.likes = obj.likes[0] }
    return obj;
})};
```
