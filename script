const startButton = document.querySelector('#start')
const screens = document.querySelectorAll('.screen')
const timeList = document.querySelector('#time-list')
const timeEl = document.querySelector('#time')
const board = document.querySelector('#board')
const customTimeStartBtn = document.querySelector('#custom-start-btn')
const customTime = document.querySelector('#custom-time')
const colors = ['#2c8a7a','#2c648a', '#592c8a', '#752c8a', '#8a2c72', '#2c8a6a']

let time = 0
let score = 0

startButton.addEventListener('click', (event) => {
    event.preventDefault()
    screens[0].classList.add('up')
})

timeList.addEventListener('click', event => {
    if (event.target.classList.contains('time-btn')) {
        time = event.target.getAttribute('data-time')
        startGame()
    }
})

customTimeStartBtn.addEventListener('click', () => {
    time = customTime.value
    startGame()
})

board.addEventListener('click', event => {
    if(event.target.classList.contains('circle')) {
        score += 10
        event.target.remove()
        createRandomTarget()
    }
})

function startGame() {
    setInterval(decreaseTime, 1000)
    createRandomTarget()
    screens[1].classList.add('up')
    setTime(time)
}

function decreaseTime() {
    if (time === 0) {
        finishGame()
    }
    else {
        let currentTime = --time
        if (currentTime < 10) {
            currentTime = `0${currentTime}`
        }
        setTime(currentTime)
    }
}

let value1 = ''
let value2 = ''

function setTime(value) {
    if (value > 59) {
        let minutes = Math.floor(value / 60)
        let seconds = value - Math.floor(minutes * 60)
        if (minutes < 10 && seconds < 10) {
            let value1 = `0${minutes}`
            let value2 = `0${seconds}`
            timeEl.innerHTML = `${value1}:${value2}`
        }
        else if (minutes < 10 && seconds > 9) {
            let value1 = `0${minutes}`
            let value2 = `${seconds}`
            timeEl.innerHTML = `${value1}:${value2}`
        }
        else if (minutes > 9 && seconds > 9) {
            let value1 = `${minutes}`
            let value2 = `${seconds}`
            timeEl.innerHTML = `${value1}:${value2}`
        }
        else if (minutes > 9 && seconds < 9) {
            let value1 = `${minutes}`
            let value2 = `0${seconds}`
            timeEl.innerHTML = `${value1}:${value2}`
        }
    }
    else {
        timeEl.innerHTML = `00:${value}`
    }
}

function finishGame() {
    timeEl.parentNode.classList.add('hide')
    board.innerHTML = `
    <div  id="score-screen">
        <h1>Ваш счёт: <span class="primary">${score}</span></h1>
        <div class="time-btn" id="restart-button">Начать сначала</div>
    </div>`
    const restartButton = document.querySelector('#restart-button')
    const scoreScreen = document.querySelector('#score-screen')

    restartButton.addEventListener('click', () => {
        restartGame()
    })
}

function restartGame() {
    location.reload()
}

function createRandomTarget() {
    const target = document.createElement('div')
    const size = getRandomNumber(8, 40)
    const {width, height} = board.getBoundingClientRect()
    const x = getRandomNumber(0, width - size)
    const y = getRandomNumber(height - size, 0)

    target.classList.add('circle')
    target.style.width = `${size}px`
    target.style.height = `${size}px`
    target.style.top = `${y}px`
    target.style.left = `${x}px`
    target.style.background = getRandomColor()

    board.append(target)
}

function getRandomNumber(min, max) {
    return Math.round(Math.random() * (max - min) + min)
}

function getRandomColor(){
    const index = Math.floor(Math.random() * colors.length)
    return colors[index]
}
