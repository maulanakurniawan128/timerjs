# PLEASE READ THIS!

This code isn't mine, but someone named [Илья Зеленько](https://stackoverflow.com/users/5286034/%d0%98%d0%bb%d1%8c%d1%8f-%d0%97%d0%b5%d0%bb%d0%b5%d0%bd%d1%8c%d0%ba%d0%be) post this on [Stackoverflow](https://stackoverflow.com/questions/21277900/how-can-i-pause-setinterval-functions/58580918#58580918) and i found it very useful. I hope his code works for whoever need it!

How to use:

```javascript
let seconds = 0
const timer = new Timer(() => {
    seconds++

    console.log('seconds', seconds)

    if (seconds === 8) {
        timer.clear()

        alert('Game over!')
    }
}, 1000)

timer.pause()
console.log('isPaused: ', timer.paused)

setTimeout(() => {
    timer.resume()
    console.log('isPaused: ', timer.paused)
}, 2500)


function Timer(callback, delay) {
    let callbackStartTime
    let remaining = 0

    this.timerId = null
    this.paused = false

    this.pause = () => {
        this.clear()
        remaining -= Date.now() - callbackStartTime
        this.paused = true
    }
    this.resume = () => {
        window.setTimeout(this.setTimeout.bind(this), remaining)
        this.paused = false
    }
    this.setTimeout = () => {
        this.clear()
        this.timerId = window.setInterval(() => {
            callbackStartTime = Date.now()
            callback()
        }, delay)
    }
    this.clear = () => {
        window.clearInterval(this.timerId)
    }

    this.setTimeout()
}
```

> The code is written quickly and did not refactored, raise the rating of my answer if you want me to improve the code and give ES2015 version (classes).
> 
> -- <cite>Илья Зеленько</cite>